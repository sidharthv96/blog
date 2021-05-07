---
title: "Getting money into India"
date: 2021-05-06T16:25:47+05:30
draft: false
toc: false
images:
tags:
  - wise.com
  - transferwise
  - payment
  - freelancer
  - international
  - forex
---

So, you just landed your first remote job and are gonna get paid in Dollars, Pounds, Yen, or any other Fiat Currency (Dogecoin does not apply).
There are multiple ways to get money into India and each has its issues. This is a summary of all the options that I evaluated along with a very helpful bunch of people at [RemoteIndian](https://remoteindian.com).

# TL;DR - My final setup

- Current account in Axis Bank
- Transfer fund as USD using Wise.com (Do NOT use INR transfer as getting FIRC is close to impossible)
- Zoho Invoice for Bookkeeping and GST
- A good Chartered Accountant for all queries

# The easy way!

Get a good CA who has experience in this area.

Having a good CA makes our lives much easier and stress-free. They'll also advise us on tax planning to boost our savings.

I had to go through 3 CAs before I finally connected with [Prasad Bhutada](mailto:prasad.bhutada@bnbca.in), another RemoteIndian member. He has in-depth knowledge in all the required areas and is extremely helpful with any queries that I have.

# Things the government wants, and how do we get them

> In this world nothing can be said to be certain, except death and taxes.
>
> - Benjamin Franklin

- Foreign Inward Remittance Certificate (FIRC)
- Income Tax
  - Quarterly Advance Tax if Tax Liability exceeds ₹10,000/-
  - Yearly Filing of ITR
- Receipts more than ₹20L:
  - GST Registration
  - Letter of Undertaking (LUT)
- Receipts more than ₹50L:
  - Audit Books under Income Tax
  - Deduct Tax at source (TDS), If hiring someone under you

## Foreign Inward Remittance Certificate

FIRC is a document provided by the Bank which acts as proof of receipt of foreign currency in your bank account. Stating the incoming currency, conversion rate, reason for transfer, and remitter details.

It is provided only when the foreign currency is transferred to your account and is issued by the Bank which processes the conversion to INR.

As software exports are taxed at 0%, FIRC is used to prove that the money was not domestic.

Getting it can be tricky when using services like Payoneer, Wise, etc. But the workaround is explained at the end.

## Income Tax

If your income is <= 50L, there is a Section 44ADA to save tax on 50% of the amount.

Check out the [Comprehensive Guide on Tax for Freelancers
](https://www.thegalacticadvisors.com/post/comprehensive-guide-on-tax-for-freelancers), written by people who know this much better than I do.

## GST and LUT

If you landed a juicy paycheck > 20L, you have to get a GST registration. Don't worry, Software and related services can be exported at 0% tax, so you don't have to pay any GST if a Letter of Undertaking is furnished. It should be submitted annually via the portal. [Simple form, few clicks, no hassle](https://cleartax.in/s/lut-letter-of-undertaking-gst).

Just get registered via the [Official portal](https://gst.gov.in) and file the Monthly GST-1 and GST-3B Forms and annual return.

Services like Zoho Invoice connects to the GST portal and make this easy. Your CA can also do it for you.

## Audits

Once your income crosses 50L, you need to get all the books audited by your CA.

## TDS

If you are hiring someone as a professional, you will have to deduct 10% from their fees if it exceeds ₹30,000/- annually and pay it as Tax Deducted at Source.

For employees, you need to deduct tax as per the slab rate,
and 10% of rent if the amount exceeds ₹2.40L annually.

You'll need to apply for a [TAN number](https://www.tin-nsdl.com/services/tan/tan-introduction.html).

# Things we want, and how do we get them

- Minimal hassle with Government
- Maximum profit ;)
- Peace of mind

# Setting up an International payment pipeline

## Choosing a Bank

This usually depends on your personal preference and relationship with them.
You will need to open a Current Account as the Forex rates are better compared to a Regular Savings account. Some banks also mandate a Current Account if you do a good amount of transactions.
There are a few points to note when selecting a bank.

### Forex Rates.

Suppose your company paid you $10,000. When you searched `10000 USD to INR` in google, it showed ₹7,36,050. But your bank only credited ₹7,16,050. Where did the ₹20k go? This is where Forex rates come into play.

Google always displays the Mid Market Rate, but your bank has a separate rate (Card Rate) which they offer to regular customers.
The card rate is always a few Rupee below the Mid Market Rate.

I've been offered ₹1 above card rate by the Person at the bank when the Card rate was ₹2 below IBR. So I would still be losing ₹1/£.

To get the best possible rates, you should always negotiate with the bank with respect to IBR/MMR (Inter-Bank Rate/Mid Market Rate) and not Card rate.

They usually offer 40p below IBR if the amount is around $5000USD. But based on your relationship manager and branch, it can go down to 25-30p, or even less if you're lucky. Don't hesitate to enquire in multiple banks and leverage one against the other. The banks need you, so you have the upper hand here.

### Customer support

Having a good relationship manager will be very helpful down the road.

Stick with one of the big private banks, ICICI, HDFC, Axis, etc.

The service quality is mainly dependent on the branch and not the bank, so ask around with your friends.

### Type of account

Opening an Exchange Earners Foreign Currency (EEFC) Account will help when dealing with Forex.

A regular current account will also suffice if the volume is low.

---

## Choosing a Payment Processor

If your client can do a Direct deposit in USD using SWIFT, you can skip this section as that's the best choice.

For the rest of us, there are some companies that offer international transfers.

All of you might have heard of Paypal and Stripe. If you don't love having money in your pocket, go for Paypal. The cut that PayPal took, including the FOREX difference came to around 11% of my First transaction.
Stripe charges around 3-4% + 2% conversion charges, reasonable for an e-Commerce site having hundreds of customers, not so great for a freelancer having one or two clients.

Two better options for getting paid are Payoneer and Wise.

### Payoneer

Payoneer is straightforward, you'll get multiple receiving accounts in different currencies, all your client has to do is a local transfer to that account. Payoneer will take a 2% cut and deposit converted INR to your account.

They used to issue e-FIRCs automatically, but some people are reporting issues with that system for a few months now.

If you have an EEFC account, customer care can link it and you can get the Foreign Currency directly into your account. So the FIRC issue won't be applicable.

Their customer support is reported as subpar, and the website is also not that great.

### Wise.com (Formerly TrasferWise)

A truly modern service, cheap (~0.4% fees!) and has good support. You don't have to create an account, only share your Account Number and SWIFT code.

The only issue I had was that it was impossible to get FIRC issued when the amount was converted to INR.

But thanks to a Friend from Remote Indian community, I found out that we can send USD directly to the account via the SWIFT network with an extra charge of around $4.

So I tried this out and it worked seamlessly! Now my bank will issue the FIRC as they are doing the conversion.

Until Revolut comes to India with their borderless account, this seems like the best choice (legally 😉).
