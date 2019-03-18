# pygopherd log analyzer

Simple log analyzer for pygopherd. Fun if you have a gopherhole and want statistics.

## Requirements

- pygopherd
- syslog of some kind
- bash 4+

## Installation

- Clone the git repository or save the shell script somewhere
- Make the script executable (`chmod +x ./pygopherstats.sh`)
- Run it providing one or more logfiles to analyze:

		./pygopherstats.sh /var/log/syslog
		./pygopherstats.sh /var/log/syslog /var/log/syslog.1
		./pygopherstats.sh /var/log/syslog.*

If you don't have a central syslog server, use poor man's ssh to get all the 
log files from all the servers:

	for host in $(dig +short a example.org); do 
		ssh -l root $host "zgrep pygopherd /var/log/syslog.*"; 
	done 2>/dev/null > gopherlog


## Example report

	# pyGopherd log analyzer
	From file: /var/log/syslog
	Hostname: example.org
	Start: Mar 18 06:29:50
	End: Mar 18 12:18:23
	----------------------------------

	# Totals
	- Hits: 800
	- IP's: 60

	# Top Tens
	## Most Popular
	    165   /
	     32   /Site_updates_raymii.org_now_on_gopher.txt
	     14   /links
	     14   /About.txt
	     10   /Viewing_PDF_docx_and_odt_files_in_Mutt.txt
	     10   /SpaceCat_Launchpad_v2_an_awesome_little_macropad.txt
	      6   /Get_json_value_with_sed.txt
	      5   /Split_keyboards_a_five_year_review_including_the_ErgoDox_EZ_Matias_Ergo_Pro_and_Kinesis_Freestyle_2.txt
	      4   /Sparkling_Network.txt
	      3   /Three_New_Nitrokeys_Pro_2_Storage_2_and_Fido_u2f.txt

	## Files per IP
	     10 66.166.122.163  /Site_updates_raymii.org_now_on_gopher.txt
	      3 66.166.122.163  /About.txt
	      3 182.259.43.98  /Viewing_PDF_docx_and_odt_files_in_Mutt.txt
	      2 79.131.39.102  /SpaceCat_Launchpad_v2_an_awesome_little_macropad.txt
	      2 66.166.122.163  /SpaceCat_Launchpad_v2_an_awesome_little_macropad.txt
	      2 182.259.43.98  /Split_keyboards_a_five_year_review_including_the_ErgoDox_EZ_Matias_Ergo_Pro_and_Kinesis_Freestyl
	e_2.txt
	      2 182.259.43.98  /Site_updates_raymii.org_now_on_gopher.txt
	      2 47.72.77.216  /About.txt
	      2 185.94.189.189  /Site_updates_raymii.org_now_on_gopher.txt
	      2 18.197.227.29  /Site_updates_raymii.org_now_on_gopher.txt

	## Gophermaps per IP
	     52 182.259.43.98  /
	     32 66.166.122.163  /
	      8 60.191.38.77  /
	      7 182.259.43.98  /links
	      5 143.179.52.12  /links
	      4 143.179.52.12  /
	      3 88.75.179.155  /
	      3 84.75.205.142  /
	      3 82.68.156.30  /
	      3 79.131.39.102  /

	## Folders per IP
	      1 182.259.43.98  /links

	## Errors:
	     54   EXCEPTION FileNotFound: '/caps.txt'
	     25   EXCEPTION TypeError'>: stat()
	     24   EXCEPTION error'>: [Errno
	     17   EXCEPTION IndexError'>: string
	     12   EXCEPTION FileNotFound: '/bout.txt'
	      2   EXCEPTION FileNotFound: '/mahua/v/20190212/8dfcb2192a5052e5a152b9d8115201af_24f3fa0cbc00474fab1610181191b09c_0.
	m3u8'
	      2   EXCEPTION FileNotFound: '/Hello
	      1   EXCEPTION FileNotFound: '/links'
	      1   EXCEPTION FileNotFound: '/ite_updates_raymii.org_now_on_gopher.txt'
	      1   EXCEPTION FileNotFound: '/favicon.ico'

	# Protocols
	    480 [GopherProtocol/FileHandler]:
	    162 [GopherProtocol/BuckGophermapHandler]:
	    128 [GopherProtocol/None]
	     16 [HTTPProtocol/BuckGophermapHandler]:
	     13 [HTTPProtocol/None]
	      1 [GopherProtocol/UMNDirHandler]:


	----------------------------------
	Simple pygopherlog analyzer by raymii.org
	License: GNU GPLv3