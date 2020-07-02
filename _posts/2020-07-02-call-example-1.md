---
layout: post
title:  "Call Example 1"
date:   2020-07-02
---

Let's go through an example of purchasing a call with the hope of profiting
by selling the underlying.  Later we'll go through an example of purchasing a
call with the hope of profiting by selling the call before it expires.

Bob wants to buy a call option for stock XYZ.  On day 0, the price of one share
of XYZ is $5.  Bob finds a call option that is trading at $1 per share of XYZ,
or $100 in total, with the following terms:

  - Maturity of 5 days (expiration on day 5)
  - Strike price of $15 per share

On day 0, Bob buys the call.  Now Bob's position is -$100, +1 Call, and 0 XYZ.

Suppose Bob is willing to exercise the option before day 5.  If the price does
not rise, there's no reason to exercise the option.  For example, if the price
of XYZ remains at $5 from day 0 to day 5, Bob could spend $500 to obtain 100
shares of XYZ, or he could exercise the option and spend $1500 to obtain 100
shares of XYZ.  In either case the share price is the same, so Bob is better off
not exercising the option.

What must happen to the share price between day 0 and day 5 for Bob to be better
off exercising the option?  It must rise.  But by how much?  After exercising
the call, Bob must be able to sell the 100 shares of XYZ for more than the combined
price of the contract (the "premium") and the cost of the 100 shares sold at the
strike price.  In this case, Bob's formula is:

  min_desired_proceeds := call_price + (100 * strike_price)
    = 100 + (100 * 15)
    = 1600

So Bob will need to make $1600 from selling the 100 shares, after exercising the
call.  Therefore Bob must anticipate that the price of XYZ will, at some point
between day 0 and day 5, exceed $1600 / 100 = $16, so that he may exercise the
call before this point and then sell the 100 shares for $16 each.*

For clarity, let's go through the entire flow of asset exchanges:

1. Bob buys the call on day 0.
   Bob's position is -$100, +1 Call, 0 XYZ.

2. The price of XYZ rises to $16 on day 3.  Bob exercises the call: he buys 100
   shares of XYZ for $15 each.
   Bob's position is -$1600, 0 Call, 100 XYZ.

3. Bob sells the shares on day 3 for $16 per share.
   Bob's position is $0, 0 Call, 0 XYZ.

If he sells his shares when they're worth exactly $16 each, he breaks even.  If
the price is higher than $16 when he sells, he profits.

In general, if the contract owner plans to possibly exercise the call and sell the
underlying, they hope that the price of the underlying increases by at least:

    delta := (strike_price + (call_price / num_units)) - orig_price

(where num_units is usually 100).

Thus, the question that the owner wants to answer is, "how confient
am I that the price of the underlying will increase by at least `delta`, before
the call contract expires?"

In other words, they hope the price of the underlying increases to at least:

    min_desired_price := (strike_price + (call_price / num_units)).

* In practice, there may be brokerage fees, and depending on the kind of order
that Bob places to sell his shares, the exchange he sells on, and the state of
the order book at the time of sale, he may not sell at exactly $16 per share.
For these reasons the sale may not result in exactly $1600.
