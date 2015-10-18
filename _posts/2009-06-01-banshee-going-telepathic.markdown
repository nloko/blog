---
comments: true
date: 2009-06-01 21:35:00
layout: post
slug: banshee-going-telepathic
title: Banshee Going Telepathic!
wordpress_id: 12
categories:
- Banshee
- Summer of Code
tags:
- Banshee
- GNOME
- SoC
- Telepathy
---

So, today brings us to the end of SoC week 1. I'd say it's been quite a productive week. Although I haven't really followed my schedule outlined in my proposal, things are going well. I had initially planned to be finishing up the bindings to the Telepathy API at the end of week 1. But, during the community bonding period, I just couldn't help myself and starting playing with things by writing some [tests](http://github.com/nloko/telepathy-sharp/tree/master). I also spent some time during the community bonding period familiarizing myself with Banshee code. So, as SoC officially started, I was armed and ready.  
  
Since a picture speaks a thousand words, I've decided to go one up and post some video. I made a screencast of what's been done so far. As shown in the video, when the new Telepathy extension loads, there is a new source category in Banshee called 'Contacts.' So, here's the play-by-play:  

  * Banshee looks for active Telepathy connections, loads up the contact roster for each connection, and represents each contact as a new child source of the 'Contacts' source
  * Presence changes are reflected
  * Membership changes such as removing/adding a contact are accounted for 
  * If a connection goes away, the sources representing the contacts are cleaned up. 
  * When a connection becomes active, contacts are again loaded as sources. 
Cool stuff! But, don't take my word for it, see for yourself!  
  
For some added excitement, I added the option to announce what Banshee is currently playing to all of your contacts. The work was slated for more towards the end of the project. But, I decided to do it now, as it was fairly easy and was a good introduction into how to play some GUI stuff in Banshee.  
  
Now, I will be taking some time look over what I've done so far. My awesome mentor, Bertrand Lorentz, has already given me some tips that I need to incorporate. In addition to that, I've got a bit of a problem I need to figure out. It looks like I've run into a [Mono bug](https://bugzilla.novell.com/show_bug.cgi?id=481687). The problem is, I can't unbox an IConvertible object NDesk.DBus returns when a DBus object returns a complex variant. For simple types, I can unbox just fine. But, if the original data type is a struct or array of structs, it's an issue. Apparently, the issue is resolved in Mono 2.4. Right now, all signs are pointing to upgrading from Mono 2.0.1 to Mono 2.4, as the Telepathy API returns variants in few places. So, if I find a way to simply workaround my current problem, I will probably run into this bug again at another point. For example:  
    
	public struct IPv4Address {
		public string address;
		public uint port;
	}

	System.Object addr = ift.ProvideFile (socket_type, socket_ac, "");
	if (socket_type == SocketAddressType.IPv4) {
		Console.WriteLine (MSG_PREFIX + "Boxed object is {0}", addr.ToString ());
		IPv4Address socket_addr = (IPv4Address)Convert.ChangeType (addr, typeof (IPv4Address));
	}
  
**Results in an explosion!**
  
    [FileTransfer] Boxed object is (su)


	Unhandled Exception: System.Reflection.TargetInvocationException:
	Exception has been thrown by the target of an invocation. --->
	System.InvalidCastException: Unknown target convertion type from NDesk.DBus.DValue to tests.IPv4Addres at System.Convert.ToType (System.Object value, System.Type conversionType, IFormatProvider provider) [0x00000] 

So, as you can see, I've got plenty to keep me busy!  
  
That's all for now! In the meantime, feel free to take a peek at my [Github repository](http://github.com/nloko/banshee/tree/gsoc), if you'd like.
