---
title: "Getting money into India - 2022 edition!"
date: 2022-08-26T00:43:31+05:30
toc: false
images:
  - "/images/money.jpg"
tags:
  - wise.com
  - transferwise
  - payment
  - freelancer
  - international
  - forex
  - ICICI
  - HDFC
  - axis
  - bank
---

![Money](/images/money.jpg "Photo by Jason Leung on Unsplash")

> I have been working remote for around 2 years now. This is an updated version of the [original post](../payment).

So, you just landed your first remote job and are gonna get paid in Dollars, Pounds, Yen, or any other Fiat Currency (Dogecoin does not apply).
There are multiple ways to get money into India and each has it's own issues. This is a summary of all the options that I evaluated along with a very helpful bunch of people at [RemoteIndian](https://remoteindian.com).

# TL;DR - My final setup

- Current account in ICICI
- Transfer fund as USD via Wise.com
- Zoho Invoice for Bookkeeping and GST
- RazorpayX for paying contractors, TDS, etc
- A good Chartered Accountant for all queries

# The easy way!

Get a good CA who has experience in this area.

Having a good CA makes our lives much easier and stress-free. They'll also advise us on tax planning to boost our savings.

I had to go through 3 CAs before I finally connected with [Prasad Bhutada](mailto:prasad.bhutada@bnbca.in), another RemoteIndian member. He has in-depth knowledge in all the required areas and is extremely helpful with any queries that I have.

> 2 Year update: Still happy with Prasad.

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

As software exports are taxed at 0% GST, FIRC is used to prove that the money was not domestic.

Getting it can be tricky when using services like Payoneer, Wise, etc. But the workaround is explained at the end.

Note: Sometimes, an FIRS (Foreign Inward Remittance Statement) is issued instead of FIRC.

## Income Tax

If your income is <= 50L, there is a Section 44ADA to save tax on 50% of the amount.

Check out the [Comprehensive Guide on Tax for Freelancers
](https://www.thegalacticadvisors.com/post/comprehensive-guide-on-tax-for-freelancers), written by people who know this much better than I do.

## GST and LUT

You need to get GST registration if:

- Any part of Income is from Export of Services, ie Contractor working for company outside India ([Mandatory](https://www.e-startupindia.com/learn/gst-registration-mandatory-for-export-of-services-in-india/), ₹20L limit is not applicable).
- Income in only from India, and is more than ₹20L (or ₹10L for [Special Category States](https://help.quicko.com/support/solutions/articles/84000350379-which-are-the-special-category-states-under-gst-))

Don't worry, Software and related services can be exported at 0% tax, so you don't have to pay any GST if a Letter of Undertaking is furnished. It should be submitted annually via the portal. [Simple form, few clicks, no hassle](https://cleartax.in/s/lut-letter-of-undertaking-gst).

Just get registered via the [Official portal](https://gst.gov.in) and file the Quarterly/Monthly GST-1 and GST-3B Forms and annual return.

Services like Zoho Invoice connects to the GST portal and make this easy. Your CA can also do it for you.

Once you have registered for GST, it is mandatory that you display your GST number on your sign board and GST certificate in a "prominent place" at the place of business. You can laminate your certificate and an A4 printout with your trade name (usually your own name) + GST number as the sign board.

> 2 Year update: Still using Zoho. Had to pay a small fine when I missed to file GST thinking I had quarterly scheme when I had monthly. Everything online, very smooth.

## Audits

Once your income crosses 50L, you need to get all the books audited by your CA.

Make sure you keep all the receipts (atleast pictures) and be ready to identify each and every transaction in your bank accounts for the CA. It was really a painful process for me to try and remember year old transactions from the statement.

## TDS

If you are hiring someone as a professional, you will have to deduct 10% from their fees if it exceeds ₹30,000/- annually and pay it as Tax Deducted at Source.

For employees, you need to deduct tax as per the slab rate,
and 10% of rent if the amount exceeds ₹2.40L annually.

You'll need to apply for a [TAN number](https://www.tin-nsdl.com/services/tan/tan-introduction.html).

I use [RazorpayX](https://x.razorpay.com) to pay the contractors. They will do the following.

- Accept invoices via mail/upload
- Automatically map to your contractor
- Deduct TDS from the amount mentioned
- Pay the remaining amount to contractor
- Pay all the deducted TDS and generate the challan.

You have to upload all the details quarterly to [TRACES](https://contents.tdscpc.gov.in/) and generate Form 16 for your contractors.

# Things we want, and how do we get them

- Minimal hassle with Government
- Maximum profit ;)
- Peace of mind

# Setting up an International payment pipeline

## Choosing a Bank

This usually depends on your personal preference and relationship with them.
You will need to open a Current Account as the Forex rates are better compared to a Regular Savings account. Some banks also mandate a Current Account if you do a good amount of transactions.
There are a few points to note when selecting a bank.

> 2 Year update: I was using Axis at first. They started increasing their rates and also had multi-day delays for the fund to get credited. One time they converted incoming GBP (~Rs 100) with USD (~Rs 74) rates. Apparently everything is done manually by a team in Mumbai.
> I switched to ICICI, which had a rocky start in the account opening part (took around 2 weeks) making me doubt my choice. But once it was opened, their service has been impeccable. They offer the best rates, convert the fund in < 3 hours (compared to day(s) in Axis) and everything is online. Their netbanking site is miles ahead of HDFC.

### Forex Rates.

Suppose your company paid you $10,000. When you searched `10000 USD to INR` in google, it showed ₹7,36,050. But your bank only credited ₹7,16,050. Where did the ₹20k go? This is where Forex rates come into play.

Google always displays the Mid Market Rate, but your bank has a separate rate (Card Rate) which they offer to regular customers.
The card rate is always a few Rupee below the Mid Market Rate.

I've been offered ₹1 above card rate by the Person at the bank when the Card rate was ₹2 below IBR. So I would still be losing ₹1/£.

To get the best possible rates, you should always negotiate with the bank with respect to IBR/MMR (Inter-Bank Rate/Mid Market Rate) and not Card rate.

They usually offer 40p below IBR if the amount is around $5000USD. But based on your relationship manager and branch, it can go down to 10-30p, or even less if you're ~~lucky~~ smart. Don't hesitate to enquire in multiple banks and leverage one against the other. The banks need you, so you have the upper hand here.

### Customer support

Having a good relationship manager will be very helpful down the road.

Stick with one of the big private banks, ICICI, Axis, HDFC, etc.

The service quality is mainly dependent on the branch and not the bank, so ask around with your friends.

### Type of account

A regular current account is enough for all purposes.

Opening an Exchange Earners Foreign Currency (EEFC) Account is necessary only if you plan on keeping the FOREX as FOREX for 30 days.

I personally did not want to have the additional pressure of trying to time the Currency market, so did not opt for EEFC.

---

## Choosing a Payment Processor

If your client can do a Direct deposit in USD using SWIFT, you can skip this section as that's the best choice.

For the rest of us, there are some companies that offer international transfers.

All of you might have heard of Paypal and Stripe. If you don't love having money in your pocket, go for Paypal. The cut that PayPal took, including the FOREX difference came to around 11% of my First transaction.
Stripe charges around 3-4% + 2% conversion charges, reasonable for an e-Commerce site having thousands of customers, not so great for a freelancer having one or two clients.

Two better options for getting paid are Payoneer and Wise.

### Payoneer

Payoneer is straightforward, you'll get multiple receiving accounts in different currencies, all your client has to do is a local transfer to that account. Payoneer will take a 2% cut and deposit converted INR to your account.

They used to issue e-FIRCs automatically, but some people are reporting issues with that system for a few months now.

If you have an EEFC account, customer care can link it and you can get the Foreign Currency directly into your account. So the FIRC issue won't be applicable (as your bank will be doing the conversion and issuing FIRC).

Their customer support is reported as subpar, and the website is also not that great.

### Wise.com (Formerly TrasferWise)

A truly modern service, cheap (~0.4% fees!) and has good support. You don't have to create an account, only share your Account Number and SWIFT code.

The only issue I had was that it was impossible to get FIRC issued when the amount was converted to INR.

But thanks to a Friend from Remote Indian community, I found out that we can send USD directly to the account via the SWIFT network with an extra charge of ~$4 + ~$20 bank charge that will depend on the banks.

To enable USD-USD transfer, your client will need to send a message to Wise to enable it as it's not done by default.

This is a template you can send to your client.

```
Hello, for payment, you can register on Wise.com. After that please go to this link:
https://wise.com/help/contact/channels/email?issue=general-how-it-works&topic=general
You can write there: Hello, can you please enable USD to USD transfer to my account?
```

So I tried this out and it worked seamlessly! Now my bank will issue the FIRC as they are doing the conversion.

Wise has launched a private beta for USD-INR conversion with FIRC. It works smoothly.
I had 2 issues with it, so I'm sticking with ICICI.

- Rates are higher than what ICICI is giving me.
- I have to upload every single invoice each time and generate a payment link.

### Contractor platforms

Ask your company if they can use platforms like OysterHR, Deel, Pilot.co, etc.
Make sure you're getting Forex transferred to your account, not converted INR.

It's beneficial for Tax purposes that you're a contractor and not an Employee (via an Employer on record). So weigh this in during your offer negotiation.

---

There was a discussion whether foreign currency is required or not in RemoteIndian.

It is still not clear, adding two documents that came up in the discussion. I will update here once there is clarity.

[Section 2(6) of IGST Act](https://tgct.gov.in/tgportal/staffcollege/download_outside.aspx?fname=Miscellaneous&type=S13I.pdf)

[C.B.I. & C. Circular No. 88/07/2019-GST](https://www.cbic.gov.in/htdocs-cbec/gst/circular-cgst-88.pdf)

---

This post is solely based on my experience. This is not financial advice. This is not tax advice. Please do your own due diligence.

---

Photo by [Jason Leung](https://unsplash.com/@ninjason?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
