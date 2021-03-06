Title: Site Launch Checklist
Date: 2010-11-04 10:20
Category: websites
Tags: general, websites
Slug: site-launch-checlist
Author: Shabda Raaj
Summary: If you have already launched your website, and checked the launch checklist here, here is the next checklist to optimize your site.

The website post launch checklist.

If you have already launched your website, and checked the launch checklist here, here is the next checklist to optimize your site.


1. Optimize your images.

Upto 90% of your page's bandwidth is used up by images. Optimizing it provides one of the best returns on your time. Smushit, http://www.smushit.com/ysmush.it/, can automate this.

Priority: High

2. Compress your CSS and JS

Generally in development, you would be working with a verbose version of your CSS and Javascript files. Depending on your technology you may have an automatic way to do this when your site is deployed. If not you can use,

http://developer.yahoo.com/yui/compressor/

Priority: High

3. Add a favicon

Favicon add a custom icon in user's bookmarks and title bar. It adds a visual identity when your users have many tabs open. You can convert your logo or a png to a favicon via

http://www.chami.com/html-kit/services/favicon/

Priority: Medium

4. Create custom 404 and 500 error pages

The default 404 and 500 error pages from the server are pretty useless. You should add a more useful page, along with your branding.

Read more http://www.useit.com/alertbox/404_improvement.html

Priority: Medium

5. Reserve social media names

Register your site's name at twitter and other social networks where you plan to interact.

Priority: Medium

6. Remove directory indexes

Many servers default to showing a full list of all your files. This can be a security issue. If you use apache you can stop this by

http://www.cyberciti.biz/faq/enabling-apache-file-directory-indexing/

Priority: Medium

7. Your admin passwords are secure

You may be using "welcome" as your admin password in development. Many web frameworks have a standard place where the admin areas are.

Not that you have important data you should change this password.

Priority: High

8. Add your site to Google Webmaster

If you add your site to Google webmaster, they will provide you data such as what are common search terms they display your website for.

http://www.google.com/webmasters/

Priority: Low

9. Spell check your website

Sites like http://www.texttrust.com/ http://checkdog.com/ can automatically check your site for any spellng errors.

Priority: Low

10. Validate your Html and CSS.

A valid html site can ease debugging your site and make it more compatible with different browsers.

Priority: Low

http://validator.w3.org/

11. Canonical urls

Ensure that your site is available at both www and non www. Some people think that www in url is not useful (http://no-www.org/). Anyway you choose, there should be one canonical url.

Priority: Low

12. Your servers doesn't allow password based ssh login

Your servers should remove password based ssh login, as they are a common vector for attack. Use public/private key login instead.

Priority: Medium


13. Remove placeholder texts.

You might have lorem ipsum or similar copy while developing. Ensure they are removed.

Tip: Search for "lorem ipsum", "todo" or "remove me".

Priority: Medium

14. Login, Admin and Payment pages are on a HTTPs page

Pages which get critical data from users should be on a HTTPS secured pages. You can get it for affordable prices from Godaddy or http://rapidssl.com/

Priority: Medium

15. Server restarts critical services on a service shutdown

Software like Supervisord, Nagios or munin can ensure that your services are automatically bought up when they go down.

http://supervisord.org/

Priority: Medium

16. Legal pages are in place

If your site jurisdiction mandates that you have a privacy policy, or a contact us page, ensure you have that in place.

Priority: Medium

17. You have stress tested your site

You should ensure that you site can take appropriate load. Apache AB, siege or a SaaS tool like browsermob.com can make this easy.

Priority: Low


(Many people before us have created a website launch checklists.)

1. http://www.boxuk.com/blog/the-ultimate-website-launch-checklist
2. http://www.conversationmarketing.com/2007/03/website_launch_checklist.htm
3. http://boagworld.com/business-strategy/pre-launch-checklist/

Here are the urls listed above.

1. http://www.smushit.com/ysmush.it/
2. http://developer.yahoo.com/yui/compressor/
3. http://www.chami.com/html-kit/services/favicon/
4. http://www.useit.com/alertbox/404_improvement.html
6. http://www.cyberciti.biz/faq/enabling-apache-file-directory-indexing/
7. http://airbrakeapp.com/pages/home
8. http://www.google.com/webmasters/
9. http://www.texttrust.com/ http://checkdog.com/
10. http://validator.w3.org/
11. http://no-www.org/
12. http://httpd.apache.org/docs/2.0/programs/ab.html
13. http://www.lipsum.com/
14. http://www.rapidssl.com/
15. http://supervisord.org/

