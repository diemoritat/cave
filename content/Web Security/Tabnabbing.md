# Tabnabbing

Tabnabbing is a cyber attack that tricks users into giving away sensitive information by impersonating a legitimate website. It's a type of phishing attack that exploits users' trust in open tabs. And while nothing is foolproof, there is a way to at least mitigate the effects: using the `noopener` and `noreferrer` attributes.

##### How it works 

- A malicious website changes the content of an inactive browser tab to look like a legitimate site

- Users may unknowingly enter credentials or make transactions when they switch back to the tab

- Attackers can use the information to steal identities, install malware, or take over accounts

![[Pasted image 20250204105427.png]]

##### Who coined the term? 

- Aza Raskin, a security researcher and design expert, coined the term in early 2010

##### Why do attackers use tabnabbing in phishing?

Traditional phishing techniques largely rely on a phishing link or a malicious attachment. If the user is educated enough or becomes suspicious and alerted, the attack fails. For example, a user may not open an attachment sent by an unknown sender, open any untrusted links.

##### Why use `noopener` and `noreferrer`?

Using `noopener` prevents bad actors and links from accessing the previous tab or window that opened the current one. This is done by setting the `Window.opener()` property to null.

Adding `noreferrer` prevents external sites from knowing that you've linked to them, which means your traffic data won't be sent their way.

#### Reference

https://www.freecodecamp.org/news/what-is-tabnabbing/
https://www.thesecuritybuddy.com/phishing/what-is-tabnabbing/