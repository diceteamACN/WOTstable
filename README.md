# WOTstable
Parcheo del add in en Visual Basic con la remediacion de las vulnerabilidades del escaneo de Pen Testing


PW --> DiceTeam2020!!


**Comandos relacionados a utilizacion de repos privados (SSH)**

## para chequear las SSH locales generadas hasta el momento

```bash
$ ls -al ~/.ssh 
```

## para generar una nueva SSH privada - local 

```bash
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com" 
```

**NOTA:** tengan en cuenta que no es un simple _Copy_ + _Paste_
la parte de **your_email@example.com** deberíamos ingresarle el mail que tenemos configurado para nuestra cuenta de Github que vamos a estar usando (notese que la cuenta de github y git deberian ser las mismas)

Luego de generar la SSH, la consola te va a estar arrojando los siguientes textos:

> Generating public/private rsa key pair.

Posteriormente, te va a solicitar en que carpeta guardarlo.
Normalmente la ruta en las que se guardan las Keys locales de SSH es en _C/Users/**miUser**/.ssh_
la terminal te va a estar sugiriendo la ruta por default:

> Enter file in which to save the key (/c/Users/manuel.ibar/.ssh/id_rsa):

**NOTA:** En caso de que tengan mas de un repositorio privado al que le tengan que generar distintas keys privadas en sus respectivas computadoras, por las dudas no usen el default porque se les pisan las llaves privadas. Por mi parte (que si uso numerosos repos privados) las subsiguientes keys las guardo como: **id_rsa(n)**, i.e: 

*id_rsa1
*id_rsa2
*id_rsa3
    .
    .
    .
 *id_rsa(n)
 
 Siguiente paso: les va a estar solicitando una passphrase:
**passphrase ref!** (me daba fiaca explicarles en criollo que es un passphrase asi que les dejo lo que encontre en google si les interesa :kissing_smiling_eyes:):
 
 >A passphrase is similar to a password. However, a password generally refers to something used to authenticate or log into a system. A password generally refers to a secret used to protect an encryption key. Commonly, an actual encryption key is derived from the passphrase and used to encrypt the protected resource.
 
El siguiente seria el prompt de la terminal: 
> Enter passphrase (empty for no passphrase): [Type a passphrase]
y les pide que lo reingresen:
> Enter same passphrase again: [Type passphrase again]

Hasta aca la generacion de la clave privada local SSH

## Ingresar la clave recien generada al agente de de SSH

En principio tenemos que verificar si el agente esta corriendo:

```bash
$ eval $(ssh-agent -s)
```

Si el prompt de la terminal les devuelve un ID, we are good 2 go, e.g:

> Agent pid 965

Lo que queda por hacer es agregar esa nueva key al agente que ya chequeamos esta corriendo:

```bash
$ ssh-add ~/.ssh/id_rsa(n)
```

**NOTA:** tengan en cuenta que no es un simple _Copy_ + _Paste_
en la ultima parte, tienen que agregar el nombre de la key que crearon al principio, yo le pongo (n) para que sepan que puede ser:

*id_rsa1
*id_rsa2
*id_rsa3
    .
    .
    .
 *id_rsa(n)

Si seguimos el paso a paso del instructivo, el prompt de la terminal les deberia devolver:

> Identity added: /C/Users/**miUser**/.ssh/id_rsa(**n**) (**mail registrado para la ssh**)

## Agregar la Key publica al repositorio de Github

una vez creadas las claves privadas en la maquina local que queremos conectar con el repo privado, tenemos que matchearla con la llave publica en el repo privado de github.
para ello tenemos que ir a la ruta en donde guardamos las llaves privadas.
Me atrevo a adivinar que si siguieron el instructivo desde el inicio, va a estar en la siguiente ruta

> /C/Users/**miUser**/.ssh/

Una vez ahi, tenemos que buscar el archivo que corresponde con el nombre de la llave privada que acabamos de crear y con la extension **.pub** (tipo de archivo _Microsoft Publisher Document_)

Ingresen el siguiente comando en la terminal de Bash:

```bash
$ clip < ~/.ssh/id_rsa.pub
``` 

Lo que hace ese comando es pegarles en el ClipBoard el output de ese file, i.e. un _Copy_ + _Paste_ del contenido ese file.
Otra opcion es abrirlo con un editor de texto cualquiera y vamos a ver que contiene un codigo de encriptacion publico.
e.g.

> ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQC/yzjbCNY8AG5DyS4PYlnENw8ZyRvkrOUFIUjifuz6qyj1e/uJu8cs9nArZjcaYYF6POnDLxXYWEbHaOud8lPGEX6CmytFDtgZ3gylSy3O7LbQpgfoMa2VO9X7hbR71H/BVhr2oIXBm3Jsi6Enu5KJHcIkQtrHOsM/HAtKaGbDRqvO8Wa5M/3U2WOiERuBvxv4mxpoNc4e8YGBGH6LM8KGaspE0uSXa3nK7uaMTeFB7DgELmp4aDOxGj3hq/0Dd0bZPJ6trNG3RsFs6sInSdhLLpq8J150MCFNY2g6oQH6sXEq/dQQ7qKJmOxHk6jFFs/+/b9imRMR8GGkK6X4aBLSZwP71qioGLienLAc8Zf1zcM8w2xv2yLfNhiD7+OIivLYZw8D2wtYjVw9NawVMaDzW19k+NfHkv3ZA2VrJ9VfRRugqWk2mLQg4bgoSIh+axF04MtOLFmdTvQT5EKevs6qswWD+mmvWA7cfsfgPLWUnUgR1J11EH0qLl7XJ2jh6XJaltvGUWsuGN9eYnJVSypnnG4A7IXC6EmzUxyWlxUBEm2rsUi+7RAUmcofHJa7bvUexkOR120a3moMicZkmgxADe6M6sipPPz71ptvHH0MkswOxRcr9p7hWd9H5AcPJztPcR3emHd/cMKpbKK0bJqAQl1B7wz5IU+Ns+sYjXyLFw== manuel.ibar@accenture.com

(Ya casi terminamos :innocent:)

## Por ultimo, y teniendo la clave de encriptacion publica de la maquina local

1. Ingresamos a la cuenta de github con la que mapeamos la key que creamos en los primeros pasos (i.e. la cuenta suscripta con el mail que ingresamos en el paso de generacion)
1. En la parte superior extrema a la derecha, en donde esta nuestro Avatar de nuestro perfil, clickeamos y vamos a **Settings**
1. Buscamos la opcion de **SSH and GPG keys**
1. Clickeamos en **New SSH Key**
1. Agregamos un titulo descriptivo para la key, e.g. _Key Correspondiente a **miRepo**_
1. Pegamos la Key que tenemos copiada en el clipBoard y la guardamos con **Add SSH key**

Y listo  :relieved: 	


