# auto-fedora
Tool for generating pre-defined fedora kickstart USB drives

This project is in development stages. Let's go then.

# Goals
  - Automate kickstart generation with environment configuration
  - Allow one-file distribution for generating full kickstarts
  - Ready to use examples, with different focusing purposes
  - Configure fedora bootable USBs to download generated kickstart file
  
# Concepts 
Python's configuration parser, a la .ini files, with some additional patterns will fit into the problem. The default kickstart is splited into 5 main components, found in "default.d" directory:
  - system
  - network
  - auth
  - storage
  - base
 
The very default is simple, just enough to install pretty much everything most people need. Altought it can be changed at "ks.d", following this rules:
  - name matches exactly, it overwrites it all
  - initial number is lower than default, it will be preppended
  - otherwise will append

# Configuration file
The main directive is `vars`. As the name says, represents the template variables. All other directives will be interpreted as variables as well, but the idea is that you have more oportunities to use this variables. Let me show an example of a post script using this principle:
```ini
[vars]
some = shit

[post]
echo I am executing bash here
echo Here too :)

[pre]
# includes the file contents
%(examples/pre.sh)
echo Back to bash
```
