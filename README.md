## dnsupdate

New in version 0.9.

This module performs dynamic DNS updates as per RFC 2136. 

<table>
<tr>
<th class="head">parameter</th>
<th class="head">required</th>
<th class="head">default</th>
<th class="head">choices</th>
<th class="head">comments</th>
</tr>
<tr>
<td>a</td>
<td>no</td>
<td></td>
<td><ul></ul></td>
<td>The <em>rdata</em> for the A resource record type (i.e. an IPv4 address)</td>
</tr>
<tr>
<td>domain</td>
<td>yes</td>
<td></td>
<td><ul></ul></td>
<td>domain name to update (e.g. www)</td>
</tr>
<tr>
<td>zone</td>
<td>yes</td>
<td></td>
<td><ul></ul></td>
<td>name of the authoritative zone (e.g. example.com)</td>
</tr>
<tr>
<td>keyalgo</td>
<td>no</td>
<td>hmac-md5</td>
<td><ul><li>hmac-md5</li><li>hmac-sha1</li><li>hmac-sha224</li><li>hmac-sha256</li><li>hmac-sha384</li><li>hmac-sha512</li></ul></td>
<td>TSIG key algorithm</td>
</tr>
<tr>
<td>mname</td>
<td>yes</td>
<td></td>
<td><ul></ul></td>
<td>address of the master server to which to send the update to. This module does not currently determine the <em>mname</em> from the zone's SOA record.</td>
</tr>
<tr>
<td>aaaa</td>
<td>no</td>
<td></td>
<td><ul></ul></td>
<td>The <em>rdata</em> for the AAAA resource record type (i.e. an IPv6 address)</td>
</tr>
<tr>
<td>secret</td>
<td>yes</td>
<td></td>
<td><ul></ul></td>
<td>secret TSIG key blob (base-64 encoded)</td>
</tr>
<tr>
<td>keyname</td>
<td>yes</td>
<td></td>
<td><ul></ul></td>
<td>name of the TSIG key required to perform updates</td>
</tr>
<tr>
<td>ttl</td>
<td>yes</td>
<td>3600</td>
<td><ul></ul></td>
<td>Time to Live for the RR.</td>
</tr>
<tr>
<td>txt</td>
<td>no</td>
<td></td>
<td><ul></ul></td>
<td>The <em>rdata</em> for the TXT resource record type. Space-separated strings are encoded as per DNS rules.</td>
</tr>
<tr>
<td>op</td>
<td>no</td>
<td>no</td>
<td><ul><li>add</li><li>delete</li><li>replace</li></ul></td>
<td>Operation to perform. add adds the specified RR to the RRset, del deletes the specified RRset and replace replaces the RRset with the RRs. If the operation is delete, the value of the RR is not verified as the <b>whole</b> RRset is deleted from the DNS.</td>
</tr>
</table>

* Example from Ansible Playbooks

```
local_action: dnsupdate keyname="mykey1"
           secret="xxxxxxxxxx=="
           mname=192.168.1.10
           zone=example.org
           domain=www
           a=${ec2_ip_address}
           op=add

```
 

#### Notes
This module requires _dnspython_ ([http://www.dnspython.org/](http://www.dnspython.org/)), and it will typically be run as a `local_action` so as to not push the secret TSIG key all over the show.
