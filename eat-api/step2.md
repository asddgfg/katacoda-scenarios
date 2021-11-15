# 2.1 supporting services by order microservice

The order microservice support various functions as follows:

First, a client sent an order to the API. The API will notify the store. After receiving a response with status code 200. The order will be inserted into the Redis database the service own. Also, it will check the event bus whether the store is active.

* /order: handle an order

`curl -X POST -v http://localhost:5000/order -H 'authorization: 740becc4b623786cc812c956a5afb30e' -H 'Content-Type: application/json' -d @./order_service/sample_order_data2.json`{{execute}}

After the order is handled, the client can conduct the operations as follows. 
* /order/<order_id>: get an order information

`curl -v http://localhost:5000/order/f9f363d1-e1c2-4595-b477-c649845bc952 -H 'authorization: 740becc4b623786cc812c956a5afb30e'`{{execute}}

* /stores/<store_id>/created-orders # get orders 

`curl -v http://localhost:5000/stores/c7f1dc2f-fabe-4997-845c-cad26fdcb894/created-orders?limit=5 -H 'authorization: 740becc4b623786cc812c956a5afb30e'`{{execute}}

* /stores/<store_id>/canceled-orders

`curl -v http://localhost:5000/stores/c7f1dc2f-fabe-4997-845c-cad26fdcb894/canceled-orders -H 'authorization: 740becc4b623786cc812c956a5afb30e'`{{execute}}

* /orders/<order_id>/accept_pos_order: accept an order

`curl -X POST -v http://localhost:5000/orders/f9f363d1-e1c2-4595-b477-c649845bc952/accept_pos_order -H 'Content-Type: application/json' -d '{"reason": "accepted"}' -H 'authorization: 740becc4b623786cc812c956a5afb30e'`{{execute}}
`
* /orders/<order_id>/deny_pos_order: deny an order

`curl -X POST -v http://localhost:5000/orders/f9f363d1-e1c2-4595-b477-c649845bc952/deny_pos_order -H 'authorization: 740becc4b623786cc812c956a5afb30e' -H 'Content-Type: application/json' -d '{ "reason": { "explanation":"failed to submit order", "code":"ITEM_AVAILABILITY", "out_of_stock_items":[ "540cb880-0286-417b-9c6c-be586fd50f76", "094f3308-4389-4ce5-bf30-ce9e09c6ed1c" ], "invalid_items":[ "1cd26db9-6be3-4b0a-9216-e4868c5d79ec" ] } }'`{{execute}}

* /orders/<order_id>/cancel: cancel an order

`curl -X POST -v http://localhost:5000/orders/f9f363d1-e1c2-4595-b477-c649845bc952/cancel -H 'authorization: 740becc4b623786cc812c956a5afb30e' -H 'Content-Type: application/json' -d '{"reason":"CANNOT_COMPLETE_CUSTOMER_NOTE","details":"note is impossible"}'`{{execute}}

* /orders/<order_id>/restaurantdelivery/status

`curl -X POST -v http://localhost:5000/orders/f9f363d1-e1c2-4595-b477-c649845bc952/restaurantdelivery/status -H 'authorization: 740becc4b623786cc812c956a5afb30e' -H 'Content-Type: application/json' -d '{"status": "delivered"}'`{{execute}}

# 2.2 unit test
To install pytest and redis

`python3 -m pip install pytest`{{execute}}

`python3 -m pip install redis`{{execute}}

Perform unit test

`python3 -m pytest -v test_order_serivce.py`{{execute}}