# SVB-Inverted-Curve-And-Bond-Risk

You are wondering what the hell happened with Silicon Valley Bank (SVB) - it sounds like they didn't invest in any toxic assets like what happened in the 2008 Subprime Crisis. It appears that much of the problem was due to

  A) taking large deposits from startups and Venture Capitalists (who get large investment money from various sources for building highly innovative tech companies from scratch),

then

  B) investing that money in bonds,

and then

  C) losing money on those bonds when those depositors tried to take their money out.

Most of these bond investments are (on the surface) _"safe investments"_ - things like (US Government-backed) Treasury bonds and fairly safe Mortgage-backed securities (not the toxic subprime mortgage derivatives of the 2008 crisis).

So what went wrong???

I will simplify the situation to make it easy to understand. I will only use high-school-level math and won't assume any knowledge of financial/investments math. We start with a little lesson of how a traditional bank used to make money, and then we understand how that strategy, seemingly safe on the surface, can lead to large losses (as what happened with SVB recently).

Back in the day, a bank would collect a lot of cash deposits from people (and institutions) who wanted to keep their money safe at the bank, and the bank would then invest that money in bonds that would fetch a healthy yield. The term investing in bonds means lending money to a bond-issuer (eg: US Government, for Treasury bonds) who will pay it back as Principal and Interest. The Principal payment is the return of the bond debt taken by the bond-issuer (Principal paid at maturity of the bond), and the Interest is typically paid twice a year until bond maturity. Let's say the bank collected $100B in deposits and paid the depositors 1% interest rate (annualized rate) on their deposits. Let's also say the bank invested in Treasury bonds that mature over several years (typically 5 or 10 or 30). Some of the longer maturity bonds fetched a healthy interest rate back in the day. Let's say the bank invested in bonds that fetched a 6% interest rate. Thus, they collect a net yield of _5% (= 6% - 1%)_ annually on the _$100B_ in deposits. This is _"free money"_ to the tune of _$5B (= $100B * 5%)_. This sounds like an amazing business. We should all start a bank. Is there a catch?

Yes, there always is. For this, I need to explain some Math. Fear not - this will be high-school math. This is known as Bond Math (not the James Bond kind though!).

A bond has a time to maturity that we refer to as _𝑇_
 (_𝑇_ can be 30 years or 10 years or 5 years or 2 years, and actually you can also do _𝑇=1_
 year, half a year or quarter of a year). We will focus on situations where _𝑇_
 is large (long-dated bonds), the typical one being 30 years. A bond also has a coupon. Back in the day, a bond holder would get paper coupons that they could take to the friendly lady at the office of the institution who issued the bond, and she would give out the money stated on the coupon. The coupon is the regular interest payment a bond-issuer must make for the money they borrowed from the bond investor (when issuing the bond to the investor). So if the coupon (call it _𝐶_) is _5%_ and a bond investor invested _1𝑀𝑓𝑜𝑟𝑚𝑎𝑡𝑢𝑟𝑖𝑡𝑦T =$ 30 years_, then each year (over 30 years), the friendly lady would give the bond investor $1M * 5% = $50,000. Typical Treasury bonds pay the coupon twice a year, but to keep things simple, we will work with once-a-year coupon payments.

The coupon is typically set to a value close to the prevailing market interest rate for the maturity of the bond (we call this market interest rate as the bond yield). So if the prevailing market interest rate (i.e., yield) for _30-year_ maturity was _6.1%_, the bond-issuer would set the coupon to the nearby round number of _6%_. To understand the relationship between maturity _𝑇_
, coupon _𝐶_ and yield (call it _𝑦_), we have to do some simple math, and specifically, we need to understand the concept of Price of a bond.

# Let us assume that the bond-investor is SVB Bank and the bond issuer is the US Government (Treasury bonds).
​
Simply put, the Price of a bond (refered to as _$P$_) is the Current Value of the future Interest (i.e., Coupon) and Principal payments. The Principal is the return of borrowed money (borrowed by the bond-issuer) and we refer to it as $B$. So, the bond-issuer has to pay the bank $B \cdot C$ as interest every year for _$T$_ years (as interest payment in the form of coupons), and at the end of _$T$_ years, also has to pay the principal _$B$_.
​
We've already said that the conceptual way to think about yield $y$ is that it's the prevailing market interest rate for the maturity of the bond. The more opaque (computational) way to think about yield $y$ is that it's the rate at which we _**discount**_ this collection of Interest and Principal payments in order to arrive at the Bond Price $P$. The calculation involves taking the future cash flows (Interest and Principal) and discounting it back to present time to arrive at current **Fair Value** of those future cash flows, and this current fair value is the Price, i.e., the money SVB Bank would give to the bond-issuer (upon bond purchase) as a fair (current) value for future Interest and Principal payments SVB bank would receive from the bond-issuer. There is a different (equivalent) way of thinking about it - instead of working back in time, move forward in time. SVB Bank is investing $P$ in the bond, and the bond-issuer gives SVB Bank cash flows in the future (Interest and Principal payments) which on average fetch an investment-growth rate (often refered to as _**return**_) equal to the yield _$y$_. Mathematically, this translates to:
​
```math

P = \frac {B \cdot C} {1+y} + \frac {B \cdot C} {(1+y)^2} + \frac {B \cdot C} {(1 + y)^3} + \ldots + \frac {B \cdot C} {(1 + y)^{T-1}} + \frac {B \cdot C + B} {(1 + y)^T}
```
​
The powers of **$(1+y)$** in the denominator are due to the fact that _$y$_ is considered to be an annualized yield.
​
**So much for the math, but intuitively remember that the yield on a bond at any point in time is just a reflection of the prevailing market interest rate for the maturity of that bond. Each maturity has it's own market interest rate, and so it gets it's own yield, which is what drives the Price of the bond for that maturity**.

The specific concept we are interested in now is the relationship between the yield 𝑦 and the Price 𝑃
. We can see from the above equation that as yield 𝑦
 increases, Price 𝑃 decreases. Let us write some code for this and plot this relationship.
