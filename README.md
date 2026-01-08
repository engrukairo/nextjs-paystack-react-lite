# paystack-react-lite

A lightweight React wrapper for Paystack payments — compatible with React 18 and above.
This repository was forked from https://github.com/alimancs/paystack-react-lite. I've edited the sample code below to make it work perfectly with NextJS (Typescript). See directions on how to use it below.

## Get Started

This React library provides a wrapper to add Paystack Payments to your React application

### Install

```npm install paystack-react-lite```
# or using pnpm
```pnpm add paystack-react-lite```
# or using yarn
```yarn add paystack-react-lite```


### Features

1. Simple and minimal Paystack integration for React and Next.js apps
2. Supports embedding Paystack payment button easily
3. Fully typed with TypeScript
4. Built for React 18+ and future-proof for React 19
5. Easy to extend with more components and hooks in the future
6. Note that all 3 implementations produce the same results.


### 1. Setup your app to use the package
Create a Custom Type Declaration file in your root folder (or anywhere Typescript can see it). For this, I created it at types/paystack-react-lite.d.ts. Add the following content to the file:
```javascript
declare module "paystack-react-lite" {
  interface PaystackConfig {
    email: string;
    amount: number;
    publicKey: string;
    reference?: string;
    metadata?: Record<string, unknown>;
    channels?: (
      | "card"
      | "bank"
      | "ussd"
      | "qr"
      | "mobile_money"
      | "bank_transfer"
    )[];
    onSuccess: (response: {
      reference: string;
      status: string;
      transaction: string;
    }) => void;
    onClose?: () => void;
  }

  export function usePaystack(
    config: PaystackConfig
  ): {
    initializePayment: () => void;
  };
}  
```
### Ensure TypeScript Picks It Up

In your tsconfig.json, add or confirm:
```javascript
{
  "compilerOptions": {
    "typeRoots": ["./types", "./node_modules/@types"]
  }
}
```
Then restart your dev server.

### 2. Create the paystack button
You can create this anywhere. I created it in my components folder.
```ts
"use client";

import { usePaystack } from "paystack-react-lite";

export default function PayButton({
  email,
  amount,
  metadata,
}: {
  email: string;
  amount: number;
  metadata: Record<string, unknown>;
}) {
  const { initializePayment } = usePaystack({
    reference: new Date().getTime().toString(), // just use any random string here for the reference
    email: email,
    amount: amount * 100,
    publicKey: "pk_test_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    channels: ["card", "bank_transfer", "ussd"],
    metadata: metadata,
    onSuccess: ({ reference }) => {
      // do whatever you want with the reference. You should most probably send the reference back to your API for verification.
      console.log(reference);
    },
    onClose: () => console.log("Payment cancelled"),
  });

  return (
    <button
      onClick={() => initializePayment()}
      className="mt-6 w-full rounded-md bg-white py-2 font-semibold text-blue-600"
    >
      Proceed to Pay
    </button>
  );
}
```

### Call the button anywhere in your main page:
Example: in page.tsx,

```ts
import PayButton from "@/components/PayButton";
export default function PaymentPage() {
  return (
    <PayButton
      email="myemail@example.org"
      amount={10000} //actual amount
      metadata={metadata}
    />
  )
}
```

With the above, the setup is complete. Adjust further according to your needs.

### Sending Metadata with Transaction
If you want to send extra metadata e.g. Transaction description, user that made the transaction. Edit your config like so:

```ts
    const config = {
       // Your required fields
          metadata: {
            custom_fields: [
                {
                    display_name: 'description',
                    variable_name: 'description',
                    value: 'Funding Wallet'
                }
                // To pass extra metadata, add an object with the same fields as above
            ]
        }
    };
```

Please checkout [Paystack Documentation](https://developers.paystack.co/docs/paystack-inline) for other available options you can add to the tag

## Deployment

REMEMBER TO CHANGE THE KEY WHEN DEPLOYING ON A LIVE/PRODUCTION SYSTEM

## Contributing

1. Fork it!
2. Create your feature branch: `git checkout -b feature-name` 
3. Commit your changes: `git commit -am 'Some commit message'`
4. Push to the branch: `git push origin feature-name`
5. Submit a pull request 😉😉

## How can I thank you?

Why not star the github repo? I'd love the attention! Why not share the link for this repository on Twitter or Any Social Media? Spread the word!

Don't forget to [follow me on X (formerly Twitter)](https://x.com/realengrukairo)!

Thanks!
Engr. Ukairo.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
