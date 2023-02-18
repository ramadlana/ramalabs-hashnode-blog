# Automatically Generating API Call Type Definitions in TypeScript.

It's time to say goodbye to creating tedious type definitions manually for API response.

Earlier when creating API calls in typescript (FE/BE), I create type definitions manually. let's say the response is like this:

```json
{
    "products": [
        {
          "id": 59,
          "title": "Spring and summershoes",
        },
        {
          "id": 88,
          "title": "TC Reusable Silicone Magic Washing Gloves",
        }
}
```

then sure, I will create definitions like this way:

```typescript
export interface IProduct {
    "products": Array<{
        id: number;
        title: string;     
    }>
}
```

okay, it's easy because the return of the JSON string from the API Server is not complex enough. but how about this:

```json
{
  "products": [
    {
      "id": 7,
      "title": "Samsung Galaxy Book",
      "description": "Samsung Galaxy Book S (2020) Laptop With Intel Lakefield Chip, 8GB of RAM Launched",
      "price": 1499,
      "discountPercentage": 4.15,
      "rating": 4.25,
      "stock": 50,
      "brand": "Samsung",
      "category": "laptops",
      "thumbnail": "https://i.dummyjson.com/data/products/7/thumbnail.jpg",
      "images": [
        "https://i.dummyjson.com/data/products/7/1.jpg",
        "https://i.dummyjson.com/data/products/7/2.jpg",
        "https://i.dummyjson.com/data/products/7/3.jpg",
        "https://i.dummyjson.com/data/products/7/thumbnail.jpg"
      ]
    },
    {
      "id": 8,
      "title": "Microsoft Surface Laptop 4",
      "description": "Style and speed. Stand out on HD video calls backed by Studio Mics. Capture ideas on the vibrant touchscreen.",
      "price": 1499,
      "discountPercentage": 10.23,
      "rating": 4.43,
      "stock": 68,
      "brand": "Microsoft Surface",
      "category": "laptops",
      "thumbnail": "https://i.dummyjson.com/data/products/8/thumbnail.jpg",
      "images": [
        "https://i.dummyjson.com/data/products/8/1.jpg",
        "https://i.dummyjson.com/data/products/8/2.jpg",
        "https://i.dummyjson.com/data/products/8/3.jpg",
        "https://i.dummyjson.com/data/products/8/4.jpg",
        "https://i.dummyjson.com/data/products/8/thumbnail.jpg"
      ]
    },
... and thousands more
}
```

Maybe you can manually type that definition, but what if maybe the API response is more complex than above ? or maybe you have hundreds of API endpoints with different structures?

### Create it automatically

To save your precious time, just use VScode called Thunder client. it's Free and it's my favorite replacement for Postman/Insomnia because it's lightweight, fast, and simple. And sure it has a code and type generator!

Let's install and try it:

URL endpoints: `https://dummyjson.com/products/search?q=Laptop`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676713549421/a931ddea-4f8e-45ae-9f68-ccf29f387661.png align="center")

Then in the right upper corner, we can see small {} bracket icons. click it

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676713734282/510125e7-ee5b-4df9-b58b-229deb1fef70.png align="center")

Now we got fetch the javascript code, and the next step is to click generate Types

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676713899423/0302da8f-2098-499e-aaa9-6df142c2e780.png align="center")

Viola! now we have a typescript interface definition without manually creating it.