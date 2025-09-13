graph TB
    subgraph "Customer Management"
        C[customers]
        A[addresses]
        C --> A
    end
    
    subgraph "Product Catalog"
        CAT[categories]
        P[products]
        PI[product_images]
        PR[product_reviews]
        
        CAT --> P
        CAT -.-> CAT
        P --> PI
        P --> PR
        C --> PR
    end
    
    subgraph "Shopping Experience"
        SC[shopping_carts]
        CI[cart_items]
        W[wishlists]
        WI[wishlist_items]
        
        C --> SC
        SC --> CI
        P --> CI
        C --> W
        W --> WI
        P --> WI
    end
    
    subgraph "Order Processing"
        O[orders]
        OI[order_items]
        PAY[payments]
        SM[shipping_methods]
        
        C --> O
        A --> O
        O --> OI
        P --> OI
        O --> PAY
    end
    
    subgraph "Promotions"
        COU[coupons]
        OC[order_coupons]
        
        O --> OC
        COU --> OC
    end
    
    subgraph "Supply Chain"
        S[suppliers]
        PS[product_suppliers]
        IT[inventory_transactions]
        
        S --> PS
        P --> PS
        P --> IT
    end
    
    %% Styling
    classDef customerGroup fill:#e1f5fe
    classDef productGroup fill:#f3e5f5
    classDef shoppingGroup fill:#e8f5e8
    classDef orderGroup fill:#fff3e0
    classDef promoGroup fill:#fce4ec
    classDef supplyGroup fill:#f1f8e9
    
    class C,A customerGroup
    class CAT,P,PI,PR productGroup
    class SC,CI,W,WI shoppingGroup
    class O,OI,PAY,SM orderGroup
    class COU,OC promoGroup
    class S,PS,IT supplyGroup
