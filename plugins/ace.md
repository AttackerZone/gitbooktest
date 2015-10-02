# ace
https://plugins.gitbook.com/plugin/ace


## Test

```
{%ace edit=true, lang='ruby'%}
# Put you ruby code here
{%endace%}
```



{%ace edit=true, lang='ruby'%}
#!/usr/bin/env ruby
#
# for hex in $(xxd -p ethernet-cable.jpg); do echo $hex | ncat -u localhost 53 ; done
# 
require 'socket'
require 'pp'

if ARGV.size < 1
  puts "[+] sudp ruby #{__FILE__} <FILENAME>"
  exit
else
  file = ARGV[0]
end

udpsoc = UDPSocket.new
udpsoc.bind('0.0.0.0', 53)

begin

  data     = ''
  data_old = ''
  
  loop do
    response = udpsoc.recvfrom(10000)
    response = response[0].force_encoding("ISO-8859-1").encode("utf-8")
    data = response.match(/[^<][a-f0-9]([a-f0-9]).*[a-f0-9]([a-f0-9])/i).to_s
    
    File.open(file, 'a') do |d|
      d.write [data].pack("H*") unless data == data_old
      pp data unless data == data_old
    end
    
    data_old = data 
  end

rescue Exception => e
  puts e
end

{%endace%}


## Result
- Desktop Editor: (Get the code messy in the editor) not the real result 
- Web Editor:  (Get the code messy in the editor)  not the real result 
- Working on Online book: Yes 

Test link on the online gitbook