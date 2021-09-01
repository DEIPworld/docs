---
description: Here you will find detailed development instructions.
---

# Developing

### New object check list

This walk-through will cover adding new object to DEIP protocol. We will use example `test_object` with following structure:

```text
# Pseudocode
test_object {
    id id;
    string name;
}
```

* In `libraries\chain\include\deip\chain\deip_object_types.hpp`:
  * Add `test_object_type` to `object_type` enum
  * Introduce `test_object` class
  * Define `oid<test_object> test_id_type` test object id type
  * Reflect `test_object_type` field in FC\_REFLECT\_ENUM
* Add `libraries\chain\include\deip\chain\test_object.hpp` and implement `test_object` class:

  ```text
    namespace deip {
    namespace chain {
  
    using deip::protocol::asset;
  
    class test_object : public object<test_object_type, test_object>
    {
        test_object() = delete;
  
    public:
  
        template <typename Constructor, typename Allocator>
        test_object(Constructor&& c, allocator<Allocator> a)
        {
            c(*this);
        }
  
        id_type id;
        fc::shared_string name;
    };
  
    struct by_name;
  
    typedef multi_index_container<test_object,
            indexed_by<ordered_unique<tag<by_id>,
                    member<test_object,
                            test_id_type,
                            &test_object::id>>,
                    ordered_unique<tag<by_name>,
                            member<test_object,
                                    fc::shared_string,
                                    &test_object::name>>>,
            allocator<test_object>>
            test_index;
    }
    }
  
    FC_REFLECT( deip::chain::test_object,
                (id)(name)
    )
  
    CHAINBASE_SET_INDEX_TYPE( deip::chain::test_object, deip::chain::test_index )
  ```

{% hint style="warning" %}
`test_object` class will not compile and will have a lot of errors until you reference it from another _.cpp/_.hpp file.
{% endhint %}

* Add `libraries\chain\include\deip\chain\dbs_test.hpp`:

  ```text
    namespace deip {
    namespace chain {
  
    ///** DB service for operations with discipline_object
    // *  --------------------------------------------
    // */
    class dbs_test : public dbs_base {
        friend class dbservice_dbs_factory;
  
        dbs_test() = delete;
  
    protected:
        explicit dbs_test(database &db);
  
    public:
        using test_refs_type = std::vector<std::reference_wrapper<const test_object>>;
  
        /** Lists all tests.
        *
        * @returns a list of test objects
        */
        test_refs_type get_tests() const;
  
        /** Get test by id
        */
        const test_object& get_test(const test_id_type id) const;
  
        /** Get test by name
        */
        const test_object& get_test_by_name(const fc::shared_string& name) const;
    };
    } // namespace chain
    } // namespace deip
  ```

* Add `libraries\chain\dbs_test.cpp`:
  * Implement db service logic:

    ```text
        #include <deip/chain/dbs_test.hpp>
        #include <deip/chain/database.hpp>
    
        #include <tuple>
    
        namespace deip {
        namespace chain {
    
        dbs_test::dbs_test(database &db)
            : _base_type(db)
        {
        }
    
        dbs_test::test_refs_type dbs_test::get_tests() const
        {
            test_refs_type ret;
    
            auto idx = db_impl().get_index<test_index>().indicies();
            auto it = idx.cbegin();
            const auto it_end = idx.cend();
            while (it != it_end)
            {
                ret.push_back(std::cref(*it));
                ++it;
            }
    
            return ret;
        }
    
        const test_object& dbs_test::get_test(const test_id_type id) const
        {
            return db_impl().get<test_object>(id);
        }
    
        const test_object& dbs_test::get_test_by_name(const fc::shared_string & name) const
        {
            return db_impl().get<test_object, by_name>(name);
        }
    
        } //namespace chain
        } //namespace deip
    ```

  * Add `dbs_test.cpp` to `libraries\chain\CMakeLists.txt` and reload CMake project so `dbs_test.cpp` is included in build target

At this stage you should have fully working `test_object` and corresponding types and `dbs_type` which is database service for `test_object`.

