---
layout: post
title: 'The Risks of Domain Squatting with GitHub Pages Subdomains'
date: "2025-06-12 10:00:00 +0200"
author: benoit
version: 1.0.0
categories: articles
comments: true
post_description: Discover the hidden risks of domain squatting with GitHub Pages subdomains and learn how to secure your custom domain by verifying it.
---

GitHub Pages is a fantastic service that allows developers to host static websites or apps directly from a Git repository for free. It's a go-to for many developers and organizations looking to showcase their projects, documentation, or personal portfolios. However, there's a hidden risk associated with using custom domains with GitHub Pages that isn't widely discussed: domain squatting.

## Understanding the Default Setup

By default, [GitHub's documentation](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site) suggests that setting up a custom subdomain for your GitHub Pages site is pretty straightforward. You simply need to create a CNAME record in your DNS settings that points to `ORGANIZATION.github.io`. This process is well-documented and seems secure at first glance.

## The Vulnerability

Here's the catch: this default setup is not as secure as it seems. Anyone can exploit this DNS record to point your custom domain to their own GitHub repository, even if they don't belong to your organization. This means that if someone else declares example.yourdomain.com as their own, they can effectively hijack your domain and serve their own content.

## The Solution: Domain Verification

To mitigate this risk, GitHub provides an [additional step for domain verification](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages). This involves creating a TXT record in your DNS settings with a unique verification key. This step ensures that only you, the domain owner, can associate your custom domain with your GitHub Pages site.

⚠️ There is two settings to verify a domain for an organization : _Organization > Settings > **Verified and approved domain**_ and  _Organization > Settings > **Pages**_. Use the second one.

### Steps to Secure Your Domain

1. **Create a CNAME Record**: Point your custom domain to `ORGANIZATION.github.io`.
2. **Verify Your Domain**: Add a TXT record to your DNS settings with the unique verification key provided by GitHub.

## Why Isn't This the Default?

It's astonishing that this verification step isn't the default configuration. The documentation briefly mentions it, but it's not highlighted as a critical security measure. This oversight can lead to potential domain squatting, where malicious actors can take control of your domain and serve harmful or misleading content.

## Conclusion

While GitHub Pages is an incredibly useful tool, it's essential to be aware of its vulnerabilities. By taking the extra step to verify your custom domain, you can protect your site from domain squatting and ensure that your content remains secure. It's high time that GitHub makes this verification process more prominent in their documentation to prevent potential misuse.

For more details, you can refer to the official GitHub documentation on [managing a custom domain for your GitHub Pages site](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site) and [verifying your custom domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages).

Stay safe and secure your domains!