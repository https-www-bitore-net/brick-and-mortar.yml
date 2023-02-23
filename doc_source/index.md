# AWS Billing User Guide

-----
*****Copyright &copy; Amazon Web Services, Inc. and/or its affiliates. All rights reserved.*****

-----
Amazon's trademarks and trade dress may not be used in 
     connection with any product or service that is not Amazon's, 
     in any manner that is likely to cause confusion among customers, 
     or in any manner that disparages or discredits Amazon. All other 
     trademarks not owned by Amazon are the property of their respective
     owners, who may or may not be affiliated with, connected to, or 
     sponsored by Amazon.

-----
## Contents
+ [What is AWS Billing?](billing-what-is.md)
+ [Getting help with AWS Billing and Cost Management](billing-get-answers.md)
+ [Getting started](billing-getting-started.md)
+ [Managing your account](change-account-settings.md)
   + [Managing an AWS account](manage-account-payment.md)
   + [Managing an account in India](manage-account-payment-aispl.md)
   + [Closing an account](close-account.md)
+ [Using the AWS Free Tier](billing-free-tier.md)
   + [Tracking your AWS Free Tier usage](tracking-free-tier-usage.md)
+ [Understanding your customer carbon footprint tool](what-is-ccft.md)
   + [Understanding your customer carbon footprint tool overview](ccft-overview.md)
   + [Understanding your carbon emission estimations](ccft-estimation.md)
+ [Viewing your bill](getting-viewing-bill.md)
   + [Viewing your monthly charges](invoice.md)
   + [Getting an invoice emailed to you](emailed-invoice.md)
+ [Managing your payments](manage-payments.md)
   + [Managing your AWS payments](manage-general.md)
      + [Managing your AWS payment methods](manage-payment-method.md)
      + [Making payments, checking unapplied funds, and viewing your payment history](manage-making-a-payment.md)
      + [Managing your credit card payment methods](manage-cc.md)
      + [Managing your ACH direct debit payment methods](manage-debit.md)
      + [Managing your AWS payments in CNY](manage-payment-cny.md)
   + [Managing your payments in India](edit-aispl-payment-method.md)
   + [Managing your payments in AWS Europe](emea-payments.md)
      + [Managing your AWS Europe payment methods](edit-emea-payment-method.md)
      + [Making payments, checking unapplied funds, and viewing your payment history in AWS Europe](manage-making-a-payment-emea.md)
      + [Managing your AWS Europe credit card payment methods](manage-cc-emea.md)
      + [Managing your AWS Europe credit card payment verifications](manage-emea-cc-verification.md)
      + [Managing your SEPA direct debit payment methods](manage-debit-emea.md)
   + [Managing your Advance Pay](manage-advancepay.md)
   + [Managing your payment profiles](manage-paymentprofiles.md)
      + [Creating your payment profiles](manage-paymentprofiles-setup.md)
      + [Editing your payment profiles](manage-paymentprofiles-edit.md)
      + [Deleting your payment profiles](manage-paymentprofiles-delete.md)
+ [Managing your purchase orders](manage-purchaseorders.md)
   + [Setting up purchase order configurations](setup-po-lineitem.md)
   + [Adding a purchase order](adding-po.md)
   + [Editing your purchase orders](edit-po.md)
   + [Deleting your purchase orders](delete-po.md)
   + [Viewing your purchase orders](viewing-po.md)
   + [Reading your purchase order details page](reading-po-details.md)
   + [Enabling purchase order notifications](notify-po-details.md)
+ [Managing your costs with AWS Cost and Usage Reports](monitoring-cur.md)
+ [Monitoring your usage and costs](monitoring-costs.md)
   + [Using the AWS Billing console dashboard](view-billing-dashboard.md)
   + [Managing your costs with AWS Cost Categories](manage-cost-categories.md)
      + [Creating cost categories](create-cost-categories.md)
      + [Tagging cost categories](tag-cost-categories.md)
      + [Viewing cost categories](view-cost-categories.md)
      + [Editing cost categories](edit-cost-categories.md)
      + [Deleting cost categories](delete-cost-categories.md)
      + [Splitting charges within cost categories](splitcharge-cost-categories.md)
   + [Using Cost Allocation Tags](cost-alloc-tags.md)
      + [AWS-Generated Cost Allocation Tags](aws-tags.md)
         + [Activating the AWS-Generated Cost Allocation Tags](activate-built-in-tags.md)
         + [Deactivating the AWS-Generated Cost Allocation Tags](deactivate-built-in-tags.md)
         + [Restrictions on AWS-Generated Cost Allocation Tags](aws-tag-restrictions.md)
      + [User-Defined Cost Allocation Tags](custom-tags.md)
         + [Activating User-Defined Cost Allocation Tags](activating-tags.md)
         + [User-Defined Tag Restrictions](allocation-tag-restrictions.md)
      + [Monthly cost allocation report](configurecostallocreport.md)
   + [Using the AWS Price List API](price-changes.md)
      + [Using the query API](using-pelong.md)
      + [Using the bulk API](using-ppslong.md)
         + [Finding prices in an offer file](procedures.md)
         + [Finding Savings Plan prices in an offer file](sp-offer-file.md)
         + [Reading an offer file](reading-an-offer.md)
         + [Reading the offer index file](reading-the-offer-index.md)
      + [Setting up notifications](price-notification.md)
   + [Logging Billing and Cost Management API calls with AWS CloudTrail](logging-using-cloudtrail.md)
   + [Avoiding unexpected charges](checklistforunwantedcharges.md)
+ [Consolidated billing for AWS Organizations](consolidated-billing.md)
   + [Consolidated billing process](useconsolidatedbilling-procedure.md)
   + [Consolidated billing in India](useconsolidatedbilling-India.md)
   + [Effective billing date](useconsolidatedbilling-effective.md)
   + [Billing and account activity](useconsolidatedbilling-activity.md)
   + [Volume discounts](useconsolidatedbilling-discounts.md)
   + [AWS credits](useconsolidatedbilling-credits.md)
   + [Reserved instances](ri-behavior.md)
      + [Billing examples for specific services](consolidatedbilling-other.md)
      + [Turning off reserved instances and Savings Plans discount sharing](ri-turn-off.md)
         + [Turning off shared reserved instances and Savings Plans discounts](ri-turn-off-process.md)
         + [Turning on shared reserved instances and Savings Plans discounts](ri-turn-on-process.md)
   + [Understanding Consolidated Bills](con-bill-blended-rates.md)
   + [AWS Support charges for accounts in an AWS Organizations](consolidatedbilling-support.md)
+ [Security in AWS Billing and Cost Management](security.md)
   + [Data protection in AWS Billing and Cost Management](data-protection.md)
   + [AWS Identity and Access Management for AWS Billing](security-iam.md)
      + [Overview of managing access permissions](control-access-billing.md)
      + [Using identity-based policies (IAM policies) for AWS Billing](billing-permissions-ref.md)
      + [AWS Billing policy examples](billing-example-policies.md)
   + [Logging and monitoring in AWS Billing and Cost Management](billing-security-logging.md)
   + [Compliance validation for AWS Billing and Cost Management](Billing-compliance.md)
   + [Resilience in AWS Billing and Cost Management](disaster-recovery-resiliency.md)
   + [Infrastructure security in AWS Billing and Cost Management](infrastructure-security.md)
+ [Quotas and restrictions](billing-limits.md)
+ [Document history](History.md)
+ [AWS glossary](glossary.md)