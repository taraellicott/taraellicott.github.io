---
layout: post
title:      "Object IDs in Ruby"
date:       2018-07-26 23:54:54 +0000
permalink:  object_ids_in_ruby
---


You might be used to seeing object ids written like this: <strong>0x007fa5429bd900</strong>. Well that is really just the hexadecimal version of this: <strong>70173881920640. </strong>

Same object id, different way of writing it.

<img class=" size-full wp-image-17 aligncenter" src="https://taraellicott.files.wordpress.com/2018/05/skitch-6.png" alt="skitch (6)" width="570" height="147" />

 

<img class="alignnone size-full wp-image-11 aligncenter" src="https://taraellicott.files.wordpress.com/2018/05/actualcheapclownanemonefish-size_restricted.gif" alt="actualcheapclownanemonefish-size_restricted" width="406" height="276" />

We've all heard it about a thousand times - everything in Ruby is an object. So, that got me thinking -- if everything is an object, does that mean that everything has an object id? And the short answer is yes. Everything in Ruby <strong>does</strong> have an object id.

<img class=" size-full wp-image-14 aligncenter" src="https://taraellicott.files.wordpress.com/2018/05/skitch-2.png" alt="skitch (2)" width="652" height="381" />

Fixnums all have object ids, as do the values <em>true</em>, <em>false</em> and <em>nil. </em>But what's weird about these ids is that they don't look anything like the ids that we are used to seeing for objects. Also they are static, so the object id for 0 will always be 1. Wait, the object id for 0 is 1? That's confusing? Yeah, it kind of is. But, surprise, surprise, there's a logic to it.

<img class=" size-full wp-image-12 aligncenter" src="https://taraellicott.files.wordpress.com/2018/05/skitch.png" alt="skitch" width="653" height="330" />

The object ids for fixnums are <em>always</em> odd. There's a pretty basic formula to figure out the object id for a fixnum:

(fixnum * 2)+ 1

So for <strong>zero</strong> it would be:

(0 * 2) + 1 = <strong>1</strong>

Since we're always multiplying by two and then adding one, we always end up with an odd object id (for fixnums).

The Fixnum 4 has an object id of 9.

4 in binary is 100. When you put that in a Fixnum, it’s got 28 zeroes in front of it for a total of 31 bits. It looks like this:

<code>0000000000000000000000000000100</code>

If you put another 1 at the end to make 32 bits it looks like this:

<code>00000000000000000000000000001001</code>

This is 9 in binary. You know - the object id for 4

Hmm, that's kind of interesting.  And so flippin' logical. It got me thinking about all those crazy long object ids that I was used to seeing. I kinda felt like a lot of those ids were even numbers, and it turns out that I was right. Ruby assigns only odd object ids to fixnums. It assigns even object ids to pretty much everything else.

<img class="alignnone size-full wp-image-16 aligncenter" src="https://taraellicott.files.wordpress.com/2018/05/skitch-4.png" alt="skitch (4)" width="657" height="453" />

So the Boolean value <em>false</em> has an object id of 0. Well, that makes sense. I don't know much about Booleans. They consist of the truth values <i>false</i> and <i>true, </i>but for computer programming purposes values are represented with the binary digits 0 (false) and 1 (true). Cool. I knew that you could represent them that way, but I never knew that it was a reference to Boolean algebra.

<em>True</em> has an object id of 20.  Yeah, I don't really get that.

<em>Nil</em> has an object id of 8. Don't get that either, but you can't win them all.

It seemed kind of trippy to me at first that the object ids of these VALUES like true/false would always stay the same. In my mind, in seemed like if I was entering true in the console multiple times, it should be treated the same way that two identical strings or hashes or arrays are treated. They are always given distinct object ids.
<h2>Why is the number 2,147,483,647 so important?</h2>
At the time of its discovery in 1811, 2,147,483,647 was the largest known prime number.

It is the maximum positive value for a 32-bit signed binary integer in computing. It is therefore the maximum value for variables declared as integers in many programming languages (like Ruby), and the maximum possible score for many video games. In 2014, the music video for"Gangnam Style"  was played so many times on Youtube that had exceeded the 32-bit integer limit had upgrade the variable to a 64-bit integer.<sup id="cite_ref-9" class="reference"></sup><sup id="cite_ref-10" class="reference"></sup>

The data type time_t, used on operating systems such as Unix, is a signed integer counting the number of seconds since the start of the Unix epoch (January 1, 1970), and is often implemented as a 32-bit integer.<sup id="cite_ref-11" class="reference"></sup> The latest time that can be represented in this form is 03:14:07 UTC on Tuesday, 19 January 2038 ( 2,147,483,647 seconds since the start of the epoch).

This means that systems using a 32-bit <code>time_t</code> type are gonna have a big problem in 2038.<sup id="cite_ref-12" class="reference"></sup>
<h3>References</h3>
Mei, Sarah. <em>Object IDs and Fixnums.</em> http://www.sarahmei.com/blog/2009/04/21/object-ids-and-fixnums/

Tennis, Caleb. <em>Ruby VALUEs and object_ids </em> http://archive.oreilly.com/pub/post/the_ruby_value_1.html
<p id="firstHeading" class="firstHeading" lang="en">Wikipedia. <em>2,147,483,647</em>. https://en.wikipedia.org/wiki/2,147,483,647</p>
