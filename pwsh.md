Don't dell me whad do do
# Alias's
	gu - get unique
	ps - get process
	gsv - get service
	measure - measure object
	diff | compare - compare object
	gm - get member
	gal - get alias
	fl - format list
	ft - format table
	sort - sort object
	select - select object\
	gc | cat | type - get content
	sc - set content
	ac - add content
	echo | write - write output

 foreach($line in $ln){ after having line1 and line2 be elements in an array

Part 1 of Looping

	$arr = @("notepad","msedge","mspaint")
	foreach ($process in $arr) {
	Start-process $process }
	get-process -name 'notepad','msedge','mspaint'
	kill -name 'notepad','msedge','mspaint'



# **HEEEELLLLPPPP!!!!!**
## looping/itteration
	$procs = "notepad", "edge", "mspaint"
	$procs | ForEach-Object { Start-Process $_ }
	Get-Process -Name notepad, edge, mspaint
	$procs | ForEach-Object { Stop-Process $_ }
	$file = "$pwd\procs.txt"
	foreach($proc in $procs){
	    get-process | Where-Object{$_.Name -like $proc} | `
	    ForEach-Object{Add-Content $file $_.Id} }
	foreach($proc in $procs){
	    get-process | Where-Object{$_.Name -like $proc} | `
	    Format-Table -Property id, name, starttime, totalprocessortime, `
	    VirtualMemorySize, WorkingSet64 }
	Get-Content .\procs.txt | ForEach-Object{Stop-process $_}
## Match
	$line1 = 'Please send model number: MO5437 to john.doe@sharklasers.com'
	$line2 = 'What model number for john.doe@sharklasers.com?'
	$pattern = '[A-Za-z]{2}\d{2,5}'
	$text = @{ line1 = $line1 ; line2 = $line2}
	$text.GetEnumerator()| foreach-object {
	    if ($_.Value -match $pattern){
	        $line=$_.key
	        Write-Host $matches[0]":Found on $line"
	        
	    }
	    else{
	        $line=$_.Key
	        Write-Host "No matches found on: $line"
	        }
	}
## Advanced Functions
	Function Get-MultiSum([array]$array,[int]$number) {
	    Begin {
	        $sum = 0
	    }
	    Process {
	        ForEach($num in $array) {
	            if($num -eq $number) {
	                continue
	            }
	            $sum += $num
	        }
	    }
	    End {
	        $sum
	    }
	}
	Function Get-LongestName {
	    Begin {
	        $count = 0
	        $states = @()
	    }
	    Process {
	        while($count -lt 3) {
	            $res = Read-Host "Enter a U.S. State"
	            $states += $res
	            $count += 1
	        }
	    }
	    End {
	        $list = $states | sort -Property Length -Descending
	        ForEach($state in $list) {
	            "$state`: " + $state.length
	        }
	    }
	}
### Regex ####
	Function Get-NetInfo {
	    $pattern = '.*?((\d{1,3}\.){3}\d{1,3})'
	    $netinfo = ipconfig
	    $ip = ipconfig |where-Object {$_ -match "ipv4$pattern"} | %{$Matches[1]}
	    $subnet = $netinfo -match "Subnet$pattern" | %{if($_ -match $pattern) {$Matches[1] }}
	    $gw = $netinfo -match "Gateway$pattern" | %{if($_ -match $pattern) {$Matches[1]}}
	    "IP: {0}`nSubnet: {1}`nGateway: {2}" -f $ip, $subnet, $gw
	}
	function get-urlinfo {
	    get-content "$HOME\Desktop\dns.txt" | Where-Object{ $_ -match 'www\..*\.(com|org|net)' } | ForEach-Object { $matches[0] } | sort | group | tee -variable b
	    ($b | measure -Property Count -Sum).Sum
	}

