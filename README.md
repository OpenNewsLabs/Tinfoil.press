# Tinfoil
=========
Here's a quick rundown of how Tinfoil (https://tinfoil.press) is set up, both technically and socially. Tinfoil uses Discourse (https://github.com/discourse), which is a relatively easy-to-use platform for starting an online forum.

Working within Discourse
---------

1) Discourse can be set up pretty easily on DigitalOcean - that's what I use. Create an account on https://digitalocean.com.

2) Create an account at Mailgun (https://mailgun.com), Mandrill (https://mandrill.zendesk.com/hc/en-us), or any inexpensive email host of your choice. You’ll use this account later to create STMP credentials that you’ll need to host your email. You'll also be required to follow some instructions about opening your server's DNS to the email provider.

3) Follow the instructions here to set up your Discourse server on a Digital Ocean droplet: https://www.digitalocean.com/community/tutorials/how-to-install-discourse-on-ubuntu-14-04

You'll plug in your SMTP credentials, contact information, URL, and customize your plugins here within the Discourse configuration in var/discourse/containers/app.yml. If all goes well, your site should be up at the URL you've specified in containers/app.yml.

4) Install an HTTPS certificate with LetsEncrypt : https://meta.discourse.org/t/setting-up-lets-encrypt-cert-with-discourse-docker/40709 - it’s much (much) easier than installing a cert the old fashioned way.

OR

4) Alternatively, install a certificate with LetsEncrypt behind nginx: https://www.digitalocean.com/community/tutorials/how-to-install-discourse-behind-nginx-on-ubuntu-14-04. (Giving yourself access to nginx is important if you want to use Tor hidden services.)

**Tor hidden services**

5) If you want to use Tor hidden services, there’s a bit of prep work. First install Tor, and configure your hidden service: https://www.torproject.org/docs/tor-hidden-service.html.en

6) Use the Onion template within your containers/app.yml. This will require nginx to forward Onion requests to port 80. https://meta.discourse.org/t/template-for-serving-through-an-onion-address-with-docker/41536



Now the hard part - building community
--------

The hard part is building a commmunity - something I continue to learn about. Some tips I've found helpful so far: 
- Establish community norms. Tell people what you envision it can be in your internal documentation, and when talking about it outside.
- Know exactly what this community will be used for, and make people feel welcome. When new people show up, say hi to everyone individually.
- Good design helps. Have a cool logo, and a color scheme that's easy to look at. Discourse makes this fairly easy. Discourse has a pretty large community at meta.discourse.org; they've done a lot of work to iron out user experience problems by now. If there are other things you'd like to see changed, you can also tinker with the front-end design yourself by goofing around under the hood.
- Start interesting threads to kick off conversation.
- Talk about it outside. Ask relevant friends and colleagues to share it. Ping them on Twitter and Slack. Post a blog about it and circulate it widely. If it's an interesting idea to the people who you think should be involved, make sure they see it.
- Once you have people involved, keep them in the loop about how the forum is progressing. Brain dump.
- People will want to talk about things BESIDES what you intended. Maybe that's okay. That means you have people who want to thave these conversations in the space you've created. If it's something you're open to, consider finding places for them to talk - create a relevant forum category that makes sense for bringing more organization to the forum.
- Think of it as an experiment; it's okay if it doesn't work. But give it a try.
