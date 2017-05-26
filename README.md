# ipTables
1)
#!/bin/bash
#Borrar todo el trafico:
~~~
read "Quieres borrar el trafico?: s/n " respuesta
if [ $respuesta = 's' ]
then
	iptables -P INPUT DROP
	iptables -P OUTPUT DROP
	iptables -P FORWARD DROP
	iptables -L -v -n
else
	echo "No se ha borrado el trafico"
fi
exit 0
~~~

2)
#!/bin/bash
#Para bloquear una ip atacante llamada 1.2.3.4:
~~~
read "La ip 1.2.3.4 no es de fiar, quieres bloquearla? : s/n" respuesta
if [ $respuesta = 's' ]
then 
	iptables -A INPUT -s 1.2.3.4 -j DROP
	iptables -A INPUT -s 192.168.0.0/24 -j DROP
else
	echo "Tu veras lo que haces"
fi
exit 0
~~~

3)
#!/bin/bash
#Reiniciar todas las reglas de iptables:
~~~
read "Quiere reiniciar las reglas? : s/n" respuesta
if [ $respuesta = 's' ]
then 
	sudo iptables-restore < /root/firewall/iptables_reset
else
	echo "No reiniciado"
fi
exit 0
~~~

4)
#!/bin/bash
#Abrir rango de puertos:
~~~
read "Quiere abrir un rango de puertos? : s/n" respuesta
if [ $respuesta = 's' ]
then 
	iptables -A INPUT -m state --state NEW -m tcp -p tcp --dport 7000:7010 -j ACCEPT
else
	echo "Puertos no abiertos"
fi
exit 0
~~~
