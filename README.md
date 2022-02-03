Stripe::Checkout::Session.create({
      mode: 'payment',
      payment_method_types: ['card'],
      payment_method_types: ['card', 'afterpay_clearpay'],
      line_items: [{
        price_data: {
          currency: 'usd',
          product_data: {
            name: 'T-shirt',
          },
          # Make sure the total amount fits within Afterpay transaction amount limits:
          # https://stripe.com/docs/payments/afterpay-clearpay#domestic-transactions-only
          unit_amount: 2000,
        },
        quantity: 1,
      }],
      shipping_address_collection: {
        # Specify which shipping countries Checkout should provide as options for shipping locations
        allowed_countries: ['AU', 'CA', 'GB', 'NZ', 'US'],
      },
      # If you already have the shipping address, provide it in payment_intent_data:
      # payment_intent_data: {
      #   shipping: {
      #     name: 'Jenny Rosen',
      #     address: {
      #       line1: '1234 Main Street',
      #       city: 'San Francisco',
      #       state: 'CA',
      #       country: 'US',
      #       postal_code: '94111',
      #     },
      #   },
      # },
      success_url: 'https://xtra.mamatude.shop/success',
      cancel_url: 'https://xtra.mamatude.shop/cancel',
    })
