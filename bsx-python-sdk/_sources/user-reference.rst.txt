User reference
==============

Core client
-----------
You must initialize a BSXInstance via it's constructor. BSXInstance will handle all the signing and authentication internally

.. code-block:: python
    
    >>> from eth_account import Account
    >>> from bsx_python_sdk import BSXInstance
    >>> wallet_private_key = "xxx"
    >>> signer_private_key = "yyy"
    >>> wallet = Account.from_key(wallet_private_key)
    >>> signer = Account.from_key(signer_private_key)
    >>> bsx_instance = BSXInstance(domain="https://api.testnet.bsx.exchange", wallet=account, signer=signer)


.. note::

    See our `REST API Overview <https://api-docs.bsx.exchange/reference/rest-overview>`_ for the testnet and mainnet domain.

Below are supported APIs to interact with BSX Exchange

- **Create an order:**

.. code-block:: python

    >>> import time
    >>> from decimal import Decimal
    >>> from bsx_python_sdk.common.types.market import CreateOrderParams, Side
    >>> params = CreateOrderParams(
        side=Side.BUY,
        product_index=3,
        price=Decimal('100.3'),
        size=Decimal('0.1'),
        time_inf_force="GTC",
        nonce=int(time.time_ns())
    )
    >>> order = bsx_instance.create_order(params=params)

- **Cancel an order by id:**

.. code-block:: python

    >>> res = bsx_instance.cancel_order_by_id(order_id="xxx")

- **Cancel an order by nonce:**

.. code-block:: python

    >>> res = bsx_instance.cancel_order_by_nonce(nonce=123)

- **Cancel multiple orders by ids:**

.. code-block:: python

    >>> res = bsx_instance.cancel_orders_by_ids(order_ids=["xxx", "yyy"])

- **Cancel multiple orders by nonces:**

.. code-block:: python

    >>> res = bsx_instance.cancel_orders_by_nonces(nonces=[123, 456])

- **Cancel multiple orders by products:**

.. code-block:: python

    >>> res = bsx_instance.cancel_orders_by_products(product_ids=["BTC-PERP", "ETH-PERP"])

- **Cancel all open orders:**

.. code-block:: python

    >>> res = bsx_instance.cancel_all_orders(product_id="BTC-PERP")

- **Get all open orders:**

.. code-block:: python

    >>> res = bsx_instance.get_open_orders(product_id="BTC-PERP")
