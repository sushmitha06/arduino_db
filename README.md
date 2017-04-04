#php code-----> saved as true.php in htdocs of xampp
<?php
    $username = "root";  
    $password = ""; 
    $server = "localhost"; // or domain
    $conn = mysql_pconnect($server, $username, $password);
    $select = mysql_select_db("work",$conn);
    $sql = "INSERT INTO work.fair (value) VALUES ('".$_GET["value"]."')";   //work db name, fair s table name
    mysql_query($sql);
?>
 obj: to use dummy values and store in db
 output: localhost/true.php?value=9
 ------ 9 s dummy value--------------
 
 
 
 #arduino code------>
 #include <SPI.h>
#include <Ethernet.h>
byte mac[] = {
  0xDE, 0xAD, 0xBE, 0xEF, 0xFE, 0xED };
IPAddress ip(192,168,0,16); //ip of arduino frm dhcp address printer

int pin = 3;  //intializing
int value; 

IPAddress server(74.125.232.128); // ip of computer incase of xampp or domain name
EthernetClient client;

void setup() {
  Serial.begin(9600);
  Ethernet.begin(mac, ip);
   }

void loop() {
 value = analogRead(pin); //reads anolog value(voltage applied) to that pin in arduino
  // dis connect s nt working
  if (client.connect(server, 80)) {
    client.print("GET /true.php?"); 
    client.print("value=");
    client.print(pin); 
    client.println(" HTTP/1.1"); 
    client.println("Host: 192.168.0.11"); //ip of computer or domain name
    client.println("Connection: close"); 
    client.println(); 
    client.println(); 
    client.stop();   
  }
else {
    // arduino cant connect
    Serial.println("--> connection failed\n");
  }
 
  delay(10000);
}
output: connection probs
reasons: windows firewall block,
php with username,password and server to no localhost all servers ((i.e) % by default) doesnt able to access dummy value in dat case
(edited using priviledge of phpmyadmin)
