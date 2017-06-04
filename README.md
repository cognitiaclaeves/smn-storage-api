# smn-storage-api
Storage portion of SMN

     # To setup the private key for play-with-docker for a user:
     ansible-playbook -i inv/hosts -e user=cognetizen playbooks/setup-key-for-pwd.yml

Stuffing TODOs here:

 - compose file to bring up a REDIS container and a DB container (mongoDB? couchDB?)
 - flask API with heartbeat that makes call to REDIS and then fetches result, and makes call to DB, if not bypassDB ( otherwise DB: Bypassed )
     - flask API that takes a JSON post to fetch data from data source
        - mandatory runtime variables: cache_type=REDIS db_type=mongoDB
        - optional runtime variables: allow_direct_query, bypass_DB
     - JSON post has a redis key name and 'query JSON'
     - unit test to prove that exact query string returns same contents as JSON request
        - must be run against instance of API that will allow_direct_query

    select * from users where ID = 16

    key: user.12.details
    query:
      type: select
      return:
        fields: [ name, id ]
      table: users
      where:
        field: id
        is: equal_to #|lt|gt|like|included_in 
        value: 16

    # TODO: How does redis handle returns with multiple responses?


smn-backend.post { 'key': 'key', 'query': { '
