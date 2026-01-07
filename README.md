# paystack-react-lite

A lightweight React wrapper for Paystack payments — compatible with React 18 and above.
This was forked from https://github.com/alimancs/paystack-react-lite, and works perfectly with NextJS (Typescript). See directions on how to use it below.

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


### 1. Using the paystack button
```javascript
  import React from 'react';
import { PaystackButton } from 'paystack-react-lite';

const config = {
  reference: new Date().getTime().toString(),
  email: 'user@example.com',
  amount: 20000, // amount in kobo (Nigerian Naira)
  publicKey: 'pk_test_xxxxxxxxxxxxxxxxxxxxxxxxxx',
  firstname: 'John',
  lastname: 'Doe',
};

export default function App() {
  return (
    <div>
      <h1>Paystack React Lite Demo</h1>
      <PaystackButton {...config}>
        Pay Now
      </PaystackButton>
    </div>
  );
}

```

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

Don't forget to [follow me on twitter](https://twitter.com/aerleeeee)!

Thanks!
Alimam Ahmed.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
