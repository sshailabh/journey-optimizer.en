---
solution: Journey Optimizer
product: journey optimizer
title: Mandatory DMARC update
description: Learn why and when you must set DMARC record in Journey Optimizer
feature: Subdomains, Channel Configuration
topic: Administration
role: Admin
level: Experienced
keywords: subdomain, domain, mail, dmarc, record

---
# Mandatory DMARC update {#dmarc-record-update}

>[!CONTEXTUALHELP]
>id="ajo_admin_dmarc_banner_link"
>title="Learn more on mandatory DMARC update"
>abstract="As part of their enforcing industry best practices, Google and Yahoo will both be requiring that you have a **DMARC record** for any domain you use to send email to them, starting on **February 1st, 2024**. <br>Consequently, you must make sure that you have DMARC record set up for all the subdomains that you have delegated to Adobe in Journey Optimizer."

As part of their enforcing industry best practices, Google and Yahoo will both be requiring that you have a **DMARC record** for any domain you use to send email to them. This new requirement is starting on **February 1st, 2024**.

Learn more on Google and Yahoo's requirement in [this section](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/additional-resources/guidance-around-changes-to-google-and-yahoo.html?lang=en#dmarc%3A){target="_blank"}.

>[!CAUTION]
>
>Failing to comply with this new requirement from Gmail and Yahoo is expected to result in emails landing into the spam folder or getting blocked.

Consequently, Adobe strongly recommends you ensure that you have DMARC record set up for all the subdomains that you have delegated to Adobe in [!DNL Journey Optimizer]. Follow the steps below that apply to your case:

* If you have [fully delegated](delegate-subdomain.md#full-subdomain-delegation) your sending subdomains to Adobe, follow either one of the two options below:

    * Set up DMARC on the parent domain of your delegated subdomains **in your hosting solution**.

    * Set up DMARC on your delegated subdomains **using the upcoming feature in the [!DNL Journey Optimizer] administration UI** - with no extra work on your hosting solution.

* If you have set up [CNAME delegation](delegate-subdomain.md#cname-subdomain-delegation) for your sending subdomains, follow either one of the two options below:
    * Set up DMARC on your subdomains or on the parent domain of your subdomains **in your hosting solution**.
    * Set up DMARC on your delegated subdomains **using the upcoming feature in the [!DNL Journey Optimizer] administration UI**. However, it will also require entry in your hosting solution. Consequently, make sure you coordinate with your IT department so that they can perform the update as soon as the [!DNL Journey Optimizer] feature is available (on January, 30). <!--and be ready on February 1st, 2024-->
    
**More details on the [!DNL Journey Optimizer] DMARC upcoming feature will come soon.**

>[!NOTE]
>
>If you have any questions or need support, contact your Adobe Deliverability Consultant or your Adobe representative.

The most recent timelines shared by Google and Yahoo are as follows:

* Google:

    * **February 2024** – Temporary bounces designed to provide warning of non-compliance will begin. Emails will still be delivered as normal after a short delay if you are not yet in compliance. If you are fully in compliance there will be no temporary bounces and you will not be affected.

    * **April 2024** – Blocks will begin for senders who are not in compliance with DMARC requirement. Only a portion of non-compliant email will be blocked at first, with the percentage blocked increasing over time.

    * **June 1st, 2024** – Any sender not in full compliance will experience blocking.

* Yahoo has not provided exact dates, but has said "the rollout of enforcement will begin in February 2024. Enforcement will be gradually rolled out".

>[!NOTE]
>
>Learn more on implementing DMARC in the [Deliverability Best Practice Guide](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/additional-resources/technotes/implement-dmarc.html#about){target="_blank"} to better understand the impact on email deliverability.