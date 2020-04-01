# SendgribApi
Envoie d'email avec django, api sendgrid

# Création de compte sendgrid

```
// se rendre sur le site de sendgrid, créer un compte et suivr les inscruction pour la création de votre api

https://sendgrid.com/

```

# Dans votre projet Django

Installer sendgrid 

### pip install sendgrid


Dans votre le fichier où est implémenté la fonction d'envoie d'email

```

// render_to_string permet de formater le contenu d'un page html en ramplaçant les différentes variables par leur valeur
from django.template.loader import render_to_string
from sendgrid import SendGridAPIClient
from sendgrid.helpers.mail import Mail
from django.contrib.sites.shortcuts import get_current_site



current_site = get_current_site(requests)
    mail_subject = 'Sujet de votre mail'
    
    // mon_mail_html.html defini le chemain d'accès au fichier partant du fait qu'on soit dans le dossier template 
    message = render_to_string('mon_mail_html.html', {
    
    // les variables à faire passer dans mon, fiichier.html
        'user': user,
        'domain': current_site.domain,
        'uid':urlsafe_base64_encode(force_bytes(user.pk)),
        'token':account_activation_token.make_token(user),
})

//composition du mail
message = Mail(
    from_email='pharaone1er@gmail.com',
    to_emails=user.email,
    subject=mail_subject,
    html_content=message)
    
try:
    sg = SendGridAPIClient('Your api key')
    response = sg.send(message)
    print("status code", response.status_code)
    print(response.body)
    print(response.headers)
except Exception as e:
    print(e.message)
    
    
```





