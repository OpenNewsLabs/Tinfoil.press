Tinfoil.press
=========
Here's a quick rundown of how Tinfoil (https://tinfoil.press) is set up, and some tips about how to get your community started.

Tinfoil uses Discourse (https://github.com/discourse), a relatively easy-to-use platform for starting an online forum. After that, we use a few extra bells and whistles - LetsEncrypt, the Auth0 plugin, and Tor hidden services. 

Working within Discourse
---------

1) I use DigitalOcean (https://digitalocean.com) to host Tinfoil.

2) It needs a mailserver. You can use any you like (e.g., https://mailgun.com, https://mandrill.zendesk.com/hc/en-us). This account is necessary for creating STMP credentials necessary to send emails to users. This also allows us to open the Discourse server's DNS to the email provider.

3) Tinfoil is installed on an Ubuntu 14.04 DigitalOcean droplet. https://www.digitalocean.com/community/tutorials/how-to-install-discourse-on-ubuntu-14-04

4) It's dockerized, and app.yml ('/var/discourse/containers/app.yml') is essentially the control tower where we can configure Discourse by plugging in SMTP credentials, contact information, the domain, and potential plugins.

My app.yml: https://github.com/OpenNewsLabs/Tinfoil.press/blob/master/app.yml

5) I added 'web.ssl.template.yml' and 'web.letsencrypt.ssl.template.yml' to the templates in app.yml to install LetsEncrypt.

**Tor hidden services**

6) Tinfoil.press has a Tor hidden service. The relevant files are the torrc and app.yml. In app.yml, I switched on 'templates/web.onion.template.yml' and assigned a variable 'DISCOURSE_ONION' as my .onion URL.

If you want to use Tor hidden services, there’s a bit of prep work. First install Tor, and configure your hidden service. 
- Install Tor ('apt-get install tor')
- If your server is on Linux, you'll generally find the relevant torrc file in /etc/tor/torrc
- Edit the file ('nano /etc/tor/torrc') to have it match the torrc file here: https://github.com/OpenNewsLabs/Tinfoil.press/blob/master/torrc
- Restart Tor when you're done ('sudo service tor restart')
- With most standard Linux setups, you'll find your .onion URL in /var/lib/tor/hidden_service/hostname
- In your Discourse app.yml, you'll need to enable 'templates/web.onion.template.yml' and assign 'DISCOURSE_ONION' as your .onion URL.
- After that, rebuild the app ('./launcher rebuild app'). After waiting, try visiting your .onion URL in Tor Browser. It should be up.

More information here:
https://www.torproject.org/docs/tor-hidden-service.html.en
https://meta.discourse.org/t/template-for-serving-through-an-onion-address-with-docker/41536

Advice on the hard part - building community
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
