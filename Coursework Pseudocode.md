# Information System Coursework Pseudocode

```pseudocode
START eCommerce

     // an class of product
     CLASS product (seller_id,product_name, product_price, product_desc, product_customisation, product_img)
          START makeProduct
               INIT name := product_name // product title
               INIT picture := product_img // the url of the picture
               INIT price : product_price // the price of the product
               INIT seller := seller_id // the name of the seller
               INIT description :=  product_desc// the description of product
               INIT customisation := product_customisation // customisation options (e.g. color, size)
          ENDPROCEDURE
     ENDCLASS

     START login()
          INIT user_id := ''
          INIT password := ''
          INIT status := FALSE // a flag representing whether a login request is successful or not

          WHILE status = FALSE 
              // an interactive form for users to input the login information
               PRINT "ID:"
               INPUT user_id
               PRINT "Password:"
               INPUT password

               // make a request to the web server
               status := server.verification(user_id,password)

               // if the login is successful
               IF status = True THEN
                    // continue to PROCEDURE catalogue
                    CALL catalogue(id)
                    BREAK
               // otherwise
               ELSE
                    OUTPUT "Login failed, please try again"
               ENDIF
          ENDWHILE
     ENDPROCEDURE

     START sellerUploadItem(user_id)
          SET product_name, product_price, product_desc, product_customisation, product_img
          SET temp_product

          INPUT product_name, product_price, product_desc, product_customisation, product_img
          temp_product := product.makeProduct(user_id,product_name, product_price, product_desc, product_customisation, product_img)

          CALL server.uploadItem(temp_product)
     ENDPROCEDURE

     START browseCatalogue(user_id)
          SET catalogue : ARRAY OF product
          SET chosen_product

          catalogue = server.requestAllProduct()

          FOR each IN catalogue
               OUTPUT each.picture, each.name, each.price
          ENDFOR
          // the user chooses one product to view
          INPUT chosen_product
          // request the product info and guide the user to the product page
          product_info = server.requestProductInfo(chosen_product)
          CALL viewProduct(user_id,product_info)
     ENDPROCEDURE

     START viewProduct(user_id,product_info)	
          SET buy_mode
          // show product info
          OUTPUT product_info.title, product_info.picture, product_info.price, product_info.seller,product_info.description, customisation

          // check if the user wants to buy or not, and how to buy
          INPUT buy_mode
          IF buy = 'buy directly' THEN
               CALL server.addCart(user_id,product_info)
          ELSEIF buy = 'auction' THEN
               CALL auction(user_id,product_info)
          ELSE // decide not to buy
               CALL browseCataloge(user_id)
          ENDIF

     START viewCart(user_id)
          SET cart : ARRAY OF product // an array of product id
          cart := server.requestCart(user_id)
          FOR item in cart
               OUTPUT item
          ENDFOR
     ENDPROCEDURE

     START auction(user_id,product_info)
          INIT bid := 0
          INIT highest_bid := 0

          highest_bid := server.requestHighestBid(product_info)
          WHILE TRUE
               // requires the user to place bid
               INPUT bid
               IF bid > highest_bid THEN
                    CALL server.placeBid(user_id,product_info,highest_bid)
                    BREAK
               ELSE
                    PRINT "Failed - lower than highest bid, please try again"
               ENDIF
          ENDWHILE
     ENDPROCEDURE

     START proceedPayment(user_id)
          INIT total := 0  // the total amount should be paid
          SET payment_detail  
          SET cart : ARRAY OF product// an array of product id
          INIT status := FALSE // a flag representing whether the transaction is successful or not

          cart = server.requestCart(user_id)
          OUTPUT cart
          // calculate the total amount
          FOR item in cart
               total := total + item.price
          ENDFOR
          OUTPUT total

          WHILE status = FALSE
               // collect payment details from users
               INPUT payment_detail

               // make the payment
               status := server.makePayment(user_id,payment_detail,total)
               IF status = TRUE THEN
                    OUTPUT "Successful!"
                    FOR item in cart
                         CALL makeShippingOrder(user_id,item)
                    ENDFOR
               ELSE
                    OUTPUT "Failed, please try again."	
               ENDIF
          ENDWHILE
     ENDPROCEDURE

     START makeShippingOrder(user_id,item)
          SET receiver_name, receiver_addr, receiver_contact
          INIT status:=FALSE
          SET order_id

          WHILE status = FALSE
               INPUT receiver_name, receiver_addr, receiver_contact, sender_name, sender_addr, sender_contact
               status, order_id := mailingServices.processMailingRequest (receiver_name, receiver_addr, receiver_contact)
               IF status = TRUE THEN
                    PRINT "Shipping order CONFIRMED!"
                    CALL shipProduct(order_id,receiver_name, receiver_addr, receiver_contact,sender_name, sender_addr, sender_contact)
               ELSE
                    PRINT "Failed, shipping order rejected, please try again"
               ENDIF
          ENDWHILE
     ENDPROCESURE

     START shipProduct(order_id,receiver_name, receiver_addr, receiver_contact,sender_name, sender_addr, sender_contact)
          SET physical_product // physical_product is the actual (physical) product sent by the seller to the buyer
          INIT status:= FALSE
          SET tracking_info // the info and status (e.g. location) of the parcel

          GET sold_product // collect the product from the seller

          REPEAT
               // attempt to deliver the parcel to receiver
               CALL mailingService.deliver(sold_product, receiver_addr)

               // get the status of the parcel
               tracking_info:=mailingService.trackParcel(order_id)

               // inform sender and receiver
               CALL mailingService.inform(sender_name,sender_contact)
               CALL mailingService.inform(receiver_name,receiver_contact)

               // check if the parcel is delivered
               status:= mailingService.checkDelivered(receiver_name, receiver_addr, receiver_contact)

          // continue delievering until delivered 
          UNTIL stutus = TRUE

          // parcel delivered, workflow terminates
     ENDPROCEDURE
     
ENDPROGRAMME

// im so tired 😪
```

