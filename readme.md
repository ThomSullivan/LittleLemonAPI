# API STRUCTURE

## /api/auth/users

    -GET method: 
        -from Anonomous:
            401 - unauthorized
        -from registered User and Manager:
            Retrieves requesting user information
        -from Superuser:
            Retrieves all Users information

## /api/auth/users/

    -POST method:
        Allows everyone to register an account when supplied with the data:
            username
            password
            email  
               
## /api/auth/token/login/

    -POST method:
        Returns authorization token for given login:
            username
            password 

## /api/auth/users/me

    -GET method:
        displays user information based on token
        NOTE a user token is required for all features of the API with the exception of registering and viewing the menu

## /api/menu-items

     
    -GET method:
        ACCPETS PARAMS: ?perpage=5-50 | ?page=1 | ?search=title or category | (acsending order)?ordering=price, category | (decending order)?ordering=-price, category
        -from Anonomous:
            displays menu items rate limit set at two per minute
        -from Users and Managers and Superuser:
            displays menu items rate limit set at 100 per minute
    -POST method:
        -from Superusers
            Creates menu item when given data:
                title
                price

## /api/menu-items/category

    
    -GET method:
        From Superusers:
            Lists all menu item categories
    -POST method:
        From Superusers:
            Adds a category given:
                slug

## /api/menu-items/{menuitemId}

    -GET method:
        Displays all details of the given {menuitemId} 
    -PATCH method:
        from Managers and Superusers:
            Toggles the featured status of the given {menuitemId}
    -DELETE method:
        from Superusers:
            Deletes the given {menuitemId}

## /api/groups/managers/users

    -GET method:
        -from Managers and Superusers:
            Lists all users in the managers group
    -POST method:
        -from Managers and Superusers:
            Adds a user to the managers group given:
                username

## /api/groups/managers/users/{userId}

    -DELETE method:
        from Managers and Superusers:
            Removes the User associated with {userId} from the managers group 

## /api/groups/delivery-crew/users

    -GET method:
        -from Managers and Superusers:
            Lists all users in the delivery crew group
    -POST method:
        -from Managers and Superusers:
            Adds a user to the delivery crew group given:
                username

## /api/groups/delivery-crew/users/{userId}

    -DELETE method:
        from Managers and Superusers:
            Removes the User associated with {userId} from the delivery crew group

## /api/cart/menu-items

    -GET method:
        from Users:
            Displays all items and quantities currently in user's cart
    -POST method:
        from Users:
            Adds a menu item to the user's cart given:
                menuitem (Id)
                quantity
    -DELETE method:
        from Users:
            If given a menuitem (Id) removes item from the cart
            If no data give removes all items from cart

## /api/orders

    -GET method:
        from Users:
            Displays orders owned by user
        from Delivery Crew:
            Displays orders assigned to delivery crew member
        from Managers and Superusers:
            Displays all orders
    -POST method:
        places an order based on items in the user's cart, and empties the cart.

## /api/orders/{orderId}

    -GET method:
        from User:
            Shows the order details associated with {orderId} details if user is owner of order.
        from Delivery crew, Managers and Superusers:
            Shows the order details associated with {orderId}
    -PATCH method:
        from from Delivery crew, Managers and Superusers:
            Toggles the status of the order associated with {orderId}
    -PUT method:
        from Managers and Superusers:
            Assigns a delivery crew to the the order associated with {orderId}
    -DELETE method:
        from Managers and Superusers:
            Deletes the order associated with {orderId}


       