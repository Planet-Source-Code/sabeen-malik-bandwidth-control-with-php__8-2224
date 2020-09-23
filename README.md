<div align="center">

## Bandwidth control with PHP


</div>

### Description

Its a pointer to someone looking for a bandwidth control mechanism via pure PHP implementation
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[sabeen malik](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/sabeen-malik.md)
**Level**          |Intermediate
**User Rating**    |5.0 (20 globes from 4 users)
**Compatibility**  |PHP 4\.0
**Category**       |[Files](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/files__8-2.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/sabeen-malik-bandwidth-control-with-php__8-2224/archive/master.zip)





### Source Code

<p>I was given a task to restrict number of downloads , divide the total bandwidth into 2 groups and control the speed of the downloads. So i came up with the idea of doing it with PHP cause mod_bandwidth or mod_throttle werent tailored for the job. Here is the part where i attempt to control the speed of the download.
 <code><font color="#000000">
 <font color="#0000BB"><br>
 <br>
 <br>
&lt;? <br />
$filedownload </font><font color="#007700">= </font><font color="#DD0000">"files/abc.exe"</font><font color="#007700">;
<br />
</font><font color="#0000BB">$time </font><font color="#007700">= </font><font color="#0000BB">10000</font><font color="#007700">;
<br />
</font><font color="#0000BB">$obytes </font><font color="#007700">= </font><font color="#0000BB">150</font><font color="#007700">*</font><font color="#0000BB">1024</font><font color="#007700">; </font><font color="#FF8000">//150k download speed restriction
<br />
</font><font color="#0000BB">$fd </font><font color="#007700">= </font><font color="#0000BB">fopen </font><font color="#007700">(</font><font color="#0000BB">$filedownload</font><font color="#007700">, </font><font color="#DD0000">"rb"</font><font color="#007700">);
<br />
while (!</font><font color="#0000BB">feof </font><font color="#007700">(</font><font color="#0000BB">$fd</font><font color="#007700">)) {
<br />
&nbsp;&nbsp;&nbsp;&nbsp;list(</font><font color="#0000BB">$usec</font><font color="#007700">, </font><font color="#0000BB">$sec</font><font color="#007700">) = </font><font color="#0000BB">explode</font><font color="#007700">(</font><font color="#DD0000">" "</font><font color="#007700">, </font><font color="#0000BB">microtime</font><font color="#007700">());&nbsp;&nbsp;&nbsp;&nbsp;
<br />
&nbsp;&nbsp;&nbsp;&nbsp;</font><font color="#0000BB">$time_start </font><font color="#007700">= </font><font color="#0000BB">$usec </font><font color="#007700">+ </font><font color="#0000BB">$sec</font><font color="#007700">;
<br />
&nbsp;&nbsp;&nbsp;&nbsp;</font><font color="#0000BB">$bytes </font><font color="#007700">= </font><font color="#0000BB">ceil</font><font color="#007700">(</font><font color="#0000BB">$obytes</font><font color="#007700">/</font><font color="#0000BB">100</font><font color="#007700">);
<br />
&nbsp;&nbsp;&nbsp;&nbsp;echo </font><font color="#0000BB">fread</font><font color="#007700">(</font><font color="#0000BB">$fd</font><font color="#007700">, </font><font color="#0000BB">$bytes</font><font color="#007700">);
<br />
&nbsp;&nbsp;&nbsp;&nbsp;</font><font color="#0000BB">flush</font><font color="#007700">();
<br />
&nbsp;&nbsp;&nbsp;&nbsp;
<br />
&nbsp;&nbsp;&nbsp;&nbsp;if(</font><font color="#0000BB">$time </font><font color="#007700">&lt; </font><font color="#0000BB">10000</font><font color="#007700">) </font><font color="#0000BB">usleep</font><font color="#007700">(</font><font color="#0000BB">10000</font><font color="#007700">-</font><font color="#0000BB">$time</font><font color="#007700">);
<br />
&nbsp;&nbsp;&nbsp;&nbsp;</font><font color="#0000BB">$i</font><font color="#007700">++;
<br />
&nbsp;&nbsp;&nbsp;&nbsp;list(</font><font color="#0000BB">$usec</font><font color="#007700">, </font><font color="#0000BB">$sec</font><font color="#007700">) = </font><font color="#0000BB">explode</font><font color="#007700">(</font><font color="#DD0000">" "</font><font color="#007700">, </font><font color="#0000BB">microtime</font><font color="#007700">());
<br />
&nbsp;&nbsp;&nbsp;&nbsp;</font><font color="#0000BB">$time_end </font><font color="#007700">= </font><font color="#0000BB">$usec </font><font color="#007700">+ </font><font color="#0000BB">$sec</font><font color="#007700">;
<br />
&nbsp;&nbsp;&nbsp;&nbsp;</font><font color="#0000BB">$time </font><font color="#007700">=</font><font color="#0000BB">ceil</font><font color="#007700">((</font><font color="#0000BB">$time_end </font><font color="#007700">- </font><font color="#0000BB">$time_start</font><font color="#007700">)*</font><font color="#0000BB">1000000</font><font color="#007700">)+</font><font color="#0000BB">10</font><font color="#007700">;
<br />
}
<br />
</font><font color="#0000BB">fclose </font><font color="#007700">(</font><font color="#0000BB">$fd</font><font color="#007700">);
<br />
</font><font color="#0000BB">?&gt;</font>
 </font> </code><br>
 <br>Basically we know how many max bytes we need to send per sec , so we calculate the time in microseconds it took for the code iteration to take place and deduct that time from 1 sec and usleep it for that long , if it took more than 1 sec to complete the iteration ( for example the user is on dialup and cannt receive 150k per sec) than dont put in the delay. <br>
 <br>
 Hope this helps someone. You can find more PHP tips on my site but this one had to be shared in a better way :)
</p>

