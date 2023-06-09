Download Link: https://assignmentchef.com/product/solved-cs3423-systems-programming-assignment-03
<br>
awk

<strong>Introduction</strong>

For this assignment you will use <strong>awk </strong>to create a program for summarizing and printing information based on the directory listing data of files and information.

You are <u>not </u>to use any other programs, utilities, or scripting languages not covered in class, unless otherwise specifically and explicitly stated in this document.

Your program should take the output from the modified ls command line seen below, and process the data in order to output the aggregate information:

ls -la –time-style=’+%Y-%m-%d %H:%M:%S’

In fact, to avoid human error and ensure you are always using the correct command line, I suggest creating and adding a new alias to your bash resource configuration file:

alias lsa=”ls -la –time-style=’+%Y-%m-%d %H:%M:%S'”

Note that the inclusion of the leading backslash ensures no other previously-defined/existing ls aliases are used; certain other options such as -h could cause your script to fail, for example.

<strong>Aggregated information requirements</strong>

The aggregated information processed from the directory listing data should consist of the following (see example later for proper output formatting):

<ul>

 <li>Per-user grouping of file-related counts found in specified directories

  <ul>

   <li>Username of the entity owning these files</li>

   <li>Total number of files found owned by this user, printing two values: all files versus hidden files</li>

   <li>Total number of directories found that are owned by this user</li>

   <li>Total number of “other” files found that are owned by this user</li>

  </ul></li>

</ul>

<em>(these items include, but are not limited to, symbolic links, FIFO’s, character or block devices, etc. Basically, anything that is not a regular file nor a directory will fall under this category)</em>

<ul>

 <li>Total file storage (in bytes) occupied by the user’s regular files.</li>

</ul>

<ul>

 <li>Itemization of the oldest and newest <strong>regular files </strong>found <em>(if no regular files exist in the listing, simply report “None” for these items. If only one regular file exists, it is reasonable to report this file as both the oldest and newest.)</em></li>

</ul>

Also note, if multiple files share the same oldest or newest timestamps, you can break the tie however you wish; there are no guidelines you must adhere to while doing so.

<ul>

 <li>Total file-related counts found in the specified directories

  <ul>

   <li>Total users owning files within these paths</li>

   <li>Total number of files found, printing two values: all files versus hidden files</li>

   <li>Total number of directories found</li>

   <li>Total number of “other” files found</li>

  </ul></li>

</ul>

<em>(these items include, but are not limited to, symbolic links, FIFO’s, character or block devices, etc. Basically, anything that is not a regular file nor a directory will fall under this category)</em>

<ul>

 <li>Total file storage (in bytes) occupied by all regular files listed.</li>

</ul>

Note: again, <strong>do not </strong>use sed , Python, or any other languages or utilities not explicitly allowed by this assignment.

Note 2: ensure to test the processing of ls listings for multiple directories, rather than just one. Such listings can be generated by passing more than one directory to ls and/or by the simple addition of the -r recursive option to the custom ls command shown previously. Two examples of such command lines can be seen here:

ls -la –time-style=’+%Y-%m-%d %H:%M:%S’ dir1 dir2 dir3 ls -lar –time-style=’+%Y-%m-%d %H:%M:%S’ dir1

or if you have defined the aforementioned alias, equivalently: lsa dir1 dir2 dir3 file1 dir4 lsa -r dir1 file1 dir2

<em>Note that these commands can also include filenames alongside the directory names on the command line as well; this is perfectly permissible and should be accounted for, hence why it was shown in the example above.</em>

<strong>Example</strong>

The example below is an excerpt from the following command, executed upon my home directory:

ls -la –time-style=’+%Y-%m-%d %H:%M:%S’ ~

<strong>Input</strong>

<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="512222383d27342225233e11373e296164">[email protected]</a>:~/courses/cs/3423/Spring20/assign3$ head -n 30 data/input.txt total 17160 drwxrwxrwt 98 root            root           528384 2020-04-07 13:38:14 . drwxr-xr-x 26 root           root 4096 2018-09-04 10:50:29 ..

drwx—— 2 pmp099 students       4096 2020-03-03 20:57:31 appInsights-nodeAIF-444c3af9<em>←&#x21aa; </em>-8e69-4462-ab49-4191e6ad1916




<table width="589">

 <tbody>

  <tr>

   <td width="82">-rw——-</td>

   <td colspan="2" width="130">1 mce237 students</td>

   <td colspan="4" width="377">199 2020-03-01 18:41:59 .build1276786824731864129.log</td>

  </tr>

  <tr>

   <td width="82">-rw——-</td>

   <td colspan="2" width="130">1 mce237 students</td>

   <td colspan="4" width="377">199 2020-03-01 20:18:42 .build291177188595028335.log</td>

  </tr>

  <tr>

   <td width="82">-rw——-</td>

   <td colspan="2" width="130">1 mce237 students</td>

   <td colspan="4" width="377">199 2020-03-01 20:10:44 .build4195866878600813549.log</td>

  </tr>

  <tr>

   <td width="82">-rw——-</td>

   <td colspan="2" width="130">1 mce237 students</td>

   <td colspan="4" width="377">199 2020-03-01 20:08:55 .build4503681510908034369.log</td>

  </tr>

  <tr>

   <td width="82">-rw——-</td>

   <td colspan="2" width="130">1 mce237 students</td>

   <td colspan="4" width="377">199 2020-03-01 18:18:44 .build4964061885086964943.log</td>

  </tr>

  <tr>

   <td width="82">-rw——-</td>

   <td colspan="2" width="130">1 mce237 students</td>

   <td colspan="4" width="377">199 2020-03-01 20:17:13 .build5474334865226720725.log</td>

  </tr>

  <tr>

   <td width="82">-rw——-</td>

   <td colspan="2" width="130">1 mce237 students</td>

   <td colspan="4" width="377">199 2020-03-01 19:08:39 .build6322670020019345604.log</td>

  </tr>

  <tr>

   <td width="82">-rw——-</td>

   <td colspan="2" width="130">1 mce237 students</td>

   <td colspan="4" width="377">420 2020-03-01 20:08:08 .build8057453026527719771.log</td>

  </tr>

  <tr>

   <td width="82">-rw——-</td>

   <td colspan="2" width="130">1 mce237 students</td>

   <td colspan="4" width="377">199 2020-03-01 20:08:32 .build8316126450060215695.log</td>

  </tr>

  <tr>

   <td width="82">-rw——-</td>

   <td colspan="2" width="130">1 mce237 students</td>

   <td colspan="4" width="377">732 2020-03-01 20:13:35 .build8317708361921336382.log</td>

  </tr>

  <tr>

   <td width="82">-rw——-</td>

   <td colspan="2" width="130">1 mce237 students</td>

   <td colspan="4" width="377">420 2020-03-01 20:07:57 .build8983757940366444429.log</td>

  </tr>

  <tr>

   <td width="82">drwxr-xr-x</td>

   <td colspan="2" width="130">3 bfn715 students</td>

   <td colspan="3" width="182">4096 2020-03-03 23:07:12</td>

   <td width="195">dlight_bfn715</td>

  </tr>

  <tr>

   <td width="82">drwx——</td>

   <td colspan="2" width="130">3 dad980 students</td>

   <td colspan="3" width="182">4096 2020-03-05 15:44:15</td>

   <td width="195">dlight_dad980</td>

  </tr>

  <tr>

   <td width="82">drwx——</td>

   <td colspan="2" width="130">3 hrb980 students</td>

   <td colspan="3" width="182">4096 2020-04-06 09:54:44</td>

   <td width="195">dlight_hrb980</td>

  </tr>

  <tr>

   <td width="82">drwx——</td>

   <td colspan="2" width="130">3 hrm102 students</td>

   <td colspan="3" width="182">4096 2020-04-06 18:43:17</td>

   <td width="195">dlight_hrm102</td>

  </tr>

  <tr>

   <td width="82">drwx——</td>

   <td colspan="2" width="130">3 kaq447 students</td>

   <td colspan="3" width="182">4096 2020-02-26 17:58:46</td>

   <td width="195">dlight_kaq447</td>

  </tr>

  <tr>

   <td width="82">drwx——</td>

   <td colspan="2" width="130">3 mce237 students</td>

   <td colspan="3" width="182">4096 2020-03-30 00:04:57</td>

   <td width="195">dlight_mce237</td>

  </tr>

  <tr>

   <td width="82">drwx——</td>

   <td colspan="2" width="130">3 mjy610 students</td>

   <td colspan="3" width="182">4096 2020-02-27 15:33:54</td>

   <td width="195">dlight_mjy610</td>

  </tr>

  <tr>

   <td width="82">drwx——</td>

   <td colspan="2" width="130">3 pdq039 students</td>

   <td colspan="3" width="182">4096 2020-04-06 18:43:48</td>

   <td width="195">dlight_pdq039</td>

  </tr>

  <tr>

   <td width="82">drwx——</td>

   <td colspan="2" width="130">3 xie192 students</td>

   <td colspan="3" width="182">4096 2020-03-23 17:47:37</td>

   <td width="195">dlight_xie192</td>

  </tr>

  <tr>

   <td width="82">drwx——</td>

   <td colspan="2" width="130">3 ynb963 students</td>

   <td colspan="3" width="182">4096 2020-04-07 13:26:46</td>

   <td width="195">dlight_ynb963</td>

  </tr>

  <tr>

   <td width="82">-rw——-</td>

   <td colspan="2" width="130">1 hrb980 students</td>

   <td colspan="3" width="182">95 2020-03-09 16:25:53</td>

   <td width="195">exec1108000877022604592.log</td>

  </tr>

  <tr>

   <td width="82">-rw——-</td>

   <td colspan="2" width="130">1 hrb980 students</td>

   <td colspan="3" width="182">74 2020-04-03 13:39:09</td>

   <td width="195">exec1218509371493740144.log</td>

  </tr>

  <tr>

   <td width="82">-rw——-</td>

   <td colspan="2" width="130">1 hrb980 students</td>

   <td colspan="3" width="182">1470 2020-03-09 13:28:36</td>

   <td width="195">exec1334040267987479302.log</td>

  </tr>

  <tr>

   <td width="82">-rw——-</td>

   <td colspan="2" width="130">1 hrb980 students</td>

   <td colspan="3" width="182">1134 2020-04-06 10:16:23</td>

   <td width="195">exec1413924165655873346.log</td>

  </tr>

  <tr>

   <td rowspan="2" width="82">-rw——……<strong>Output</strong></td>

   <td colspan="2" width="130">1 mce237 students</td>

   <td colspan="3" rowspan="3" width="182">1538 2020-03-01 18:17:50</td>

   <td rowspan="3" width="195">exec1520228248140431728.log</td>

  </tr>

  <tr>

   <td width="75"></td>

   <td rowspan="2" width="55"></td>

  </tr>

  <tr>

   <td colspan="2" width="157">user: mjy610 dirs: 3user: hrb980 files:</td>

  </tr>

  <tr>

   <td colspan="2" width="157">all/hidden:dirs: 3</td>

   <td width="55">( 195</td>

   <td width="18">/</td>

   <td width="18">2</td>

   <td width="146">)</td>

   <td width="195"></td>

  </tr>

  <tr>

   <td colspan="2" width="157">file storage:user: pdq039 dirs: 3user: zqu051 files:</td>

   <td width="55">76235</td>

   <td width="18">B</td>

   <td width="18"></td>

   <td width="146"></td>

   <td width="195"></td>

  </tr>

  <tr>

   <td colspan="2" width="157">all/hidden:</td>

   <td width="55">( 452</td>

   <td width="18">/</td>

   <td width="18">0</td>

   <td width="146">)</td>

   <td width="195"></td>

  </tr>

  <tr>

   <td colspan="2" width="157">file storage:user: mce237 files:</td>

   <td width="55">652583</td>

   <td colspan="2" width="37">B</td>

   <td width="146"></td>

   <td width="195"></td>

  </tr>

  <tr>

   <td colspan="2" width="157">all/hidden:dirs: 4</td>

   <td width="55">( 52 /</td>

   <td colspan="2" width="37">12</td>

   <td width="146">)</td>

   <td width="195"></td>

  </tr>

  <tr>

   <td colspan="2" width="157">file storage:</td>

   <td colspan="3" width="92">2729344 B</td>

   <td width="146"></td>

   <td width="195"></td>

  </tr>

 </tbody>

</table>

user: dad980 files:

all/hidden: ( 4 / 1 )

dirs: 3 file storage: 6614 B

user: pmp099 dirs: 2

<h1>other: 10</h1>

<h1>user: ynb963 files:</h1>

<h2>all/hidden: ( 2 / 0 )</h2>

dirs: 3

file storage: 4202 B

user: xie192 dirs: 3

user: kaq447 files:

all/hidden: ( 2 / 0 )

dirs: 3 file storage: 3092 B

user: bfn715 dirs: 3

user: root files:

all/hidden: ( 1 / 1 )

dirs: 5 other: 1 file storage: 11 B

user: hrm102 dirs: 3

oldest file:

-r–r–r– 1 root                  root                                          11 2020-02-25 15:30:11 .<em>←&#x21aa;</em>

X0-lock newest file:

-rw——- 1 ynb963 students         1308 2020-04-06 19:40:46 <em>←&#x21aa; </em>output1586220046526

total users:                    13

total files all/hidden: ( 708 / 16 )

total dirs:          38 total other:  11 file storage:  3472081 B

<strong>Extra Credit (15%)</strong>

A 15% bonus will be awarded for those whose script correctly and properly sorts the usernamegrouped portion of the output. Such sorted output for the above example can be seen here:

<strong>Extra Credit Output</strong>

user: bfn715 dirs: 3

user: dad980 files:

all/hidden: ( 4 / 1 )

dirs: 3 file storage: 6614 B

user: hrb980 files:

all/hidden: ( 195 / 2 )

dirs: 3 file storage: 76235 B

user: hrm102 dirs: 3

user: kaq447 files:

all/hidden: ( 2 / 0 )

dirs: 3 file storage: 3092 B

user: mce237 files:

all/hidden: ( 52 / 12 )

dirs: 4

file storage: 2729344 B

user: mjy610 dirs: 3

user: pdq039 dirs: 3

user: pmp099 dirs: 2 other: 10

user: root files:

all/hidden: ( 1 / 1 )

dirs: 5 other: 1 file storage: 11 B

user: xie192 dirs: 3

user: ynb963 files:

all/hidden: ( 2 / 0 )

dirs: 3

file storage: 4202 B

user: zqu051 files:

all/hidden: ( 452 / 0 )

file storage: 652583 B

oldest file:

-r–r–r– 1 root                  root                                          11 2020-02-25 15:30:11 .<em>←&#x21aa;</em>

X0-lock newest file:

-rw——- 1 ynb963 students         1308 2020-04-06 19:40:46 <em>←&#x21aa; </em>output1586220046526

total users:                    13

total files all/hidden: ( 708 / 16 )

total dirs:          38 total other:  11 file storage:  3472081 B <em>Hint: research awk’s asort function for help.</em>

<strong>Script Execution</strong>

Your program should each be invoked through a single bash file (see below) with input taken from stdin. The resulting output should be printed directly to stdout.

<strong>Assignment Data</strong>

A few sample input files can be found at the following location on the fox servers, however it is imperative that you fabricate many of your own examples to ensure that your script functions <em>according to the specifications outlined above</em>:

<strong>/usr/local/courses/ssilvestro/cs3423/Spring20/assign3</strong>.

<strong>Script Files</strong>

Your submission should consist of exactly two files:

<ul>

 <li><strong>sh </strong>– a bash script used as the driver program for your awk script</li>

 <li><strong>awk </strong>– the awk program used in assign3.sh</li>

</ul>

<strong>Verifying Your Program</strong>

In addition to the above Assignment Data, your program should also work with arbitrary input from the ls -la –time-style=’+%Y-%m-%d %H:%M:%S’ command defined on page 1. This include both reading from one or more input files, as well as accepted piped input directly from standard input, as in these examples:

ls -la –time-style=’+%Y-%m-%d %H:%M:%S’ ~ | ./assign3.sh

– or – ./assign3.sh listing.txt [listing2.txt […]]


