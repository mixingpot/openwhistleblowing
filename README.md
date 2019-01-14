# Openwhistleblowing

## Introduzione
Questo repository contiene il codice sorgente e il binario pronto per
l'installazione di Openwhistleblowing (release 1.0.1), il software fornito per
il riuso dall'ANAC (Autoritá Nazionale Anti Corruzione).

## Installazione
Al fine di consentire la piú ampia personalizzazione alle Amministrazioni
utilizzatrici del software, lo stesso viene fornito completo di source. É
possibile installarlo seguendo una delle seguenti modalità:

- installazione mediante rpm (RedHat Package Manager)
- installazione utilizzando Docker
- installazione da source (utilizzando maven)

I prerequisiti per l'installazione sono:
- sistema operativo RedHat Enterprise  Linux o Centos 7.*
- 100 GB di disco per lo storage di allegati
- 4 GB RAM (suggeriti 8)

### RPM
L'installazione mediante RPM si effettua o utilizzando lo script presente in src/scripts/install.sh,
oppure lanciando manualmente le seguenti istruzioni:

```bash
cd openwhistleblowing
yum -y install epel-release
yum -y install https://download.postgresql.org/pub/repos/yum/9.6/redhat/rhel-6-x86_64/pgdg-centos96-9.6-3.noarch.rpm
yum -y install postgresql96-devel
yum -y install ../../binary/owb-1.0.1-1.x86_64.rpm &> /dev/null
```
La configurazione del tool inizialmente puó essere effettuata mediante l'utilizzo dello script
presente in src/scripts/setup.sh . Per ulteriori opzioni di configurazioni, riferirsi alla documentazione
tecnica di progetto.

### Docker
L'installazione mediante docker presuppone che Docker sia installato e funzionante (
riferirsi alla documentazione per [RedHat](https://docs.docker.com/install/linux/docker-ee/rhel/) o
[Centos](https://docs.docker.com/install/linux/docker-ce/centos/)).
Il primo step consiste nel creare l'immagine del container
```bash
cd openwhistleblowing
docker build -t owb:anac .
```
successivamente si puó far partire il container con il seguente comando (per la personalizzazione
del comando di partenza del container si rimanda alla documentazione specifica di docker)
```bash
docker run -d --restart=unless-stopped --name=owb -p 80:80 -v /data:/var/owb/files owb:anac
```
per la successiva configurazione é possibile entrare nel container in esecuzione:
```bash
docker exec -it owb /bin/bash
```
effettuare le modifiche e far ripartire il tool con:
```bash
/etc/init.d/owb restart
```

### Source
L'installazione da source permette la piú ampia customizzazione dell'applicativo. Viene
fornito il pom.xml per la creazione dell'rpm che verrà successivamente installato come
da istruzioni precedenti.
Per la pacchettizzazione é necessario installare [maven](https://maven.apache.org/) e 
lanciare il seguente comando:
```bash
cd openwhistleblowing
mvn package
```
alla fine dell'esecuzione il nuovo rpm generato si troverà nel path:
*target/rpm/owb/RPMS/x86_64/*