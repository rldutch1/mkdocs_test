#Heading
<pre>
----------------:
	<span style="color: #3366ff;">
	-------------
	</span>

Bacula Services:
<span style="color: #3366ff;">
	service bacula-dir start
	service bacula-fd start
	service bacula-sd start

	systemctl enable bacula-dir
	systemctl enable bacula-fd
	systemctl enable bacula-sd

	systemctl status bacula-dir
	systemctl status bacula-fd
	systemctl status bacula-sd

	ss -lt <-(Should show all three services listening)
</span>
</pre>
<pre>
Bacula Cheat Sheet
Bacula is a nifty backup software that is network-capable and stores data in <br />the database for faster retrieval in case you need a certain file back. <br />As a big fan of cheat sheets I created this cheat sheet.

What’s up?
Which files shall be backed up?	<span style="color: #3366ff;">show filesets	I=Included, E=Excluded</span>
What’s the server doing?	<span style="color: #3366ff;">status dir</span>
What’s the status of a certain job?	<span style="color: #3366ff;">status jobid=xx</span>
What’s the client doing?	<span style="color: #3366ff;">status client</span>
What’s the streamer doing?	<span style="color: #3366ff;">status storage</span>
Anything new?	<span style="color: #3366ff;">messages</span>

Backing up:
Start a backup	<span style="color: #3366ff;">run	…and choose the backup job</span>
Label a new tape	<span style="color: #3366ff;">label	…and run mount afterwards</span>

Restoring:
The common way (a user accidentally removed a file and wants the newest version back from the tapes:

Use the restore command.
Choose option 5 (Select the most recent backup for a client).
Commands:
	<span style="color: #3366ff;">cd</span>
	<span style="color: #3366ff;">ls</span>
	<span style="color: #3366ff;">dir</span>
	<span style="color: #3366ff;">mark</span>
	<span style="color: #3366ff;">markdir</span>
	<span style="color: #3366ff;">unmark</span>
	<span style="color: #3366ff;">unmarkdir</span>
	<span style="color: #3366ff;">lsmark</span>
	<span style="color: #3366ff;">estimate</span>
	<span style="color: #3366ff;">pwd</span>
	<span style="color: #3366ff;">count</span>
	<span style="color: #3366ff;">find</span> can use <span style="color: #3366ff;">find *</span> to show the files.
	<span style="color: #3366ff;">done</span>

Jobs
Last jobs	<span style="color: #3366ff;">list jobs</span>	…or <span style="color: #3366ff;">list jobid=xx</span> for a specific job

Statistics about last jobs	<span style="color: #3366ff;">list jobtotal</span>

Which files were backed up?	<span style="color: #3366ff;">list files jobid=xx</span>

Job status
Status	means…
	<span style="color: #3366ff;">T</span>	Terminated normally
	<span style="color: #3366ff;">C</span>	Created but not yet running
	<span style="color: #3366ff;">R</span>	Running
	<span style="color: #3366ff;">B</span>	Blocked
	<span style="color: #3366ff;">E</span>	Terminated in Error
	<span style="color: #3366ff;">e</span>	Non-fatal error
	<span style="color: #3366ff;">f</span>	Fatal error
	<span style="color: #3366ff;">D</span>	Verify Differences
	<span style="color: #3366ff;">A</span>	Canceled by the user
	<span style="color: #3366ff;">F</span>	Waiting on the File daemon
	<span style="color: #3366ff;">S</span>	Waiting on the Storage daemon
	<span style="color: #3366ff;">m</span>	Waiting for a new Volume to be mounted
	<span style="color: #3366ff;">M</span>	Waiting for a Mount
	<span style="color: #3366ff;">s</span>	Waiting for Storage resource
	<span style="color: #3366ff;">j</span>	Waiting for Job resource
	<span style="color: #3366ff;">c</span>	Waiting for Client resource
	<span style="color: #3366ff;">d</span>	Wating for Maximum jobs
	<span style="color: #3366ff;">t</span>	Waiting for Start Time
	<span style="color: #3366ff;">p</span>	Waiting for higher priority job to finish
	<span style="color: #3366ff;">W</span>	Terminated with warnings

Tapes (bconsole commands)
  <span style="color: #3366ff;">add</span> - Assign a tape to a certain pool.
  <span style="color: #3366ff;">delete media</span> - Remove a tape.
  <span style="color: #3366ff;">list files jobid=nn</span> - List the files that were saved for JobId nn.
  <span style="color: #3366ff;">list jobid=rn</span> - Lists JobId nn from the Catalog.
  <span style="color: #3366ff;">list jobmedia</span> - List the media information for each Job run.
  <span style="color: #3366ff;">list jobs</span> - Lists all jobs in the Catalog that have run.
  <span style="color: #3366ff;">list jobtotals</span> - Lists totals for all jobs in the Catalog.
  <span style="color: #3366ff;">list media</span> - Lists all the media defined in the Catalog.
  <span style="color: #3366ff;">list pools</span> - List the pools defined in the Catalog (normally only
  Default is used).
  <span style="color: #3366ff;">list volumes</span> - Shows the volumes that bconsole knows about.
  <span style="color: #3366ff;">messages</span> - Prints any messages that have been directed to the
  console.
  <span style="color: #3366ff;">mount storage=storage-name</span> - Causes the drive associated with
  the storage device to be mounted again. When Bacula reaches the end of a volume and requests you to
  mount a new volume, you must issue this command after you have placed the new volume in the drive.
  In effect, it is the signal needed by Bacula to know to start reading or writing the new volume.
  <span style="color: #3366ff;">quit</span> - Exit or quit the console program.
  <span style="color: #3366ff;">reload</span> - Reload changes from the bacula-xx.conf files.
  <span style="color: #3366ff;">status dir</span> - Print a status of all running jobs and jobs scheduled
  in the next 24 hours.
  <span style="color: #3366ff;">status jobid=rn</span> - Print a status of JobId nn if it is running.
  The Storage daemon is contacted and requested to print a current status of the job as well.
  <span style="color: #3366ff;">status</span> - The console program will prompt you to select a daemon
  type, then will request the daemon's status.
  <span style="color: #3366ff;">show client status</span> - Show the status of clients.
  <span style="color: #3366ff;">show dir status</span> -
  <span style="color: #3366ff;">show filesets</span> -
  <span style="color: #3366ff;">show storage</span> -
  <span style="color: #3366ff;">unmount storage=storage-name</span> - Unmounts the drive associated
  with the storage device with the name storage-name if the drive is not currently being used. This
  command is used if you wish Bacula to free the drive so that you can use it to label a tape.
  <span style="color: #3366ff;">update volume</span> - Change parameters of a tape.
Most of the commands given above, with the exception of list, will prompt you for the necessary
arguments if you simply enter the command name.

Terminology
<span style="color: #3366ff;">Catalog</span>
It is data in a SQL database running on the server. The catalog stores information about all assets
like jobs, clients and media. Without the catalog Bacula had no idea which files were backed up and
cannot restore them. In case of a disastrous loss of the catalog you need to take the latest bootstrap
and start restoring the catalog first using that information. So the catalog itself is also backed up
because without it the system is useless.

<span style="color: #3366ff;">Volumes</span>
Volumes (also called “media”) are either files on disk or physical tapes. When backups run they save
their data to volumes. Bacula keeps track in the catalog which data can be found on each volume.
Usually multiple backups run in parallel leading to a multiplexed stream of data written to volumes.
A volume always belongs to exactly one pool. Volumes have names/labels – tapes have the name that
is printed on the barcode sticker if the library have a barcode scanner.

<span style="color: #3366ff;">Pool</span>
A set of volumes. The pool can define a maximum number of volumes, the type of volumes (e.g. disk
or tape) and the retention period. For example you can have short-lived disk pools for small frequent
backups. On the other hand you may have long-lived tape pools that store data for several weeks or
months.

<span style="color: #3366ff;">Job</span>
A specific action like a backup, restore or copy (e.g. from disk to tape). Jobs are usually started
automatically by the director following a pre-defined schedule. Multiple jobs can run in parallel
and share their resources. The catalog keeps track of which jobs have run in the past in order to
know which volumes would be required to restore data from them.

In the bconsole you can see the running, past and scheduled jobs by running “stat dir”.

<span style="color: #3366ff;">Job definition (aka jobdef)</span>
The definition of a job. It is not stored in the catalog but in text files in /etc/bacula.

<span style="color: #3366ff;">Client</span>
A server to be backed up. Usually a file-daemon runs on the client. The director will talk to the
client to run jobs.

<span style="color: #3366ff;">Fileset</span>
Defines which files or directories to backup from a certain server. A job defines which fileset to
use for a backup.

<span style="color: #3366ff;">Bootstrap</span>
A small text file usually sent out via email frequently. It is required in case of a catalog loss to
find the volume that contains the last backup of the catalog.

The upstream documents reads: “The bootstrap ﬁle contains ASCII information that permits precise
speciﬁcation of what ﬁles should be restored, what volume they are on, and where they are on the
volume. It is a relatively compact form of specifying the information, is human readable, and can be
edited with any text editor.”

The bootstrap data is not confidential and should be forwarded to an external location in case of a
disaster.

<span style="color: #3366ff;">Message</span>
Bacula can send messages to the console or via email. Results of jobs are sent via email.

<span style="color: #3366ff;">Schedule</span>
A definition of how often and at what time a job can be run.

<span style="color: #3366ff;">Storage</span>
Defines a way to write volumes. It is used by the storage daemon. A storage can be a path on the
local disks or the name of the tape device. Autochangers (aka “tape libraries”) are also supported.

<span style="color: #3366ff;">Retention</span>
A volume is locked after being written to. The retention period defines when the volume can be
overwritten again.

<span style="color: #3366ff;">Scratch</span>
This applies to tape volumes only. New tapes can be introduced into the “Scratch” pool. If a pool
is out of volumes to use then Bacula will take a volume from the Scratch pool and take it into its
own pool.

<span style="color: #3366ff;">Levels</span>
Backups can happen in three different levels: Full, Differential and Incremental. Only Full backups
are required. The other levels can be used to save space on volumes.

Full: every single file defined in assigned fileset is saved to the volume
Differential: only new files that were not contained in the last Full backup are backed up
Incremental: only new files that were not contained in the last Differential or Incremental backup
are backed up
Using only Full backups is secure because if you lose a full backup then you take the full backup
before it. However you are stubbornly backing up the same files time and again thus wasting space
on the volumes. Complete restores are fastest though because only the last full backup has to be
considered.

Using Full and Differential backups saves some space. During restores the last Full and last
Differential backup are considered. However multiple Differential backups may store files
redundantly thus wasting a little space.

Using Full and Incremental backups saves most space. However for a restore all Incremental backups
since the last Full backup need to be working. If one Incremental backup is broken in the chain
then only the last Full backup can be restored.

Using Full + Differential + Incremental backups saves most space while still keeping the risk of
losing data low. A restore requires the Incremental backups back up to the last Differential
backup + the last Full backup. This could look like:

Full
Differential
Incremental
Incremental
Incremental
Incremental
Differential
Incremental
Incremental
Incremental <–
Incremental
Full
…
To restore the highlighted Incremental backup you would need the previous Differential and Full
backups printed in bold letters.

Which mode to use depends on the type of data to backup. Database directories usually change in
its entirety so a Full backup is the best solution. File servers with millions of files gain some
advantage from using Full, Differential and Incremental backups.

Dangerous configurations:

Using a rare Full backup and rely on many intermediate Incremental backups. If any of the many
Incremental backups were faulty you would lose all data back to that time.
Losing the Full backup and only keeping Incremental backups. This may occur if the retention
periods are not adequately configured for Full backups.

Eject the tape.
		<span style="color: #3366ff;">mt -f /dev/st0 eject</span>

		For bacula: use bconsole to unmount the tape drive then exit the program and eject the tape
		using the command above.
		username@servername:/home/username
		$ <span style="color: #3366ff;">sudo bconsole</span>
				<span style="color: #3366ff;">*unmount</span>
				Automatically selected Catalog: MyCatalog
				Using Catalog "MyCatalog"
				The defined Storage resources are:
		    		 1: File1
		    		 2: File2
		    		 3: LTO-4
		    		 4: LTO-4_SD
				Select Storage resource (1-4): <span style="color: #3366ff;">4</span>
				3001 Device ""LTO-4" (/dev/st0)" unmounted.
				*<span style="color: #3366ff;">quit</span>
		username@servername:/home/username
				$ <span style="color: #3366ff;">mt -f /dev/st0 eject</span>
		username@servername:/home/username
		$ <span style="color: #3366ff;">sudo bconsole</span>
				*<span style="color: #3366ff;">mount</span>
				Automatically selected Catalog: MyCatalog
				Using Catalog "MyCatalog"
				The defined Storage resources are:
				     1: File1
				     2: File2
				     3: LTO-4
				     4: LTO-4_SD
				Select Storage resource (1-4): <span style="color: #3366ff;">4</span>
				3001 Device ""LTO-4" (/dev/st0)" is mounted with Volume "Tape-0004"
				You have messages.



Troubleshooting
Erase a label on the tape	<span style="color: #3366ff;">mt rewind && mt weof && mt rewind</span>

Tape drive full and could not be written to:
Solution was to use bconsole to unmount, then eject the tape from the commandline, then insert
Tape-0004 and mount from bconsole.
27-May 08:00 bacula-sd JobId 219: Warning: Director wanted Volume "Tape-0004".
    Current Volume "Tape-0003" not acceptable because:
    1998 Volume "Tape-0003" catalog status is Error, but should be Append, Purged or Recycle.

    I think the command "mount storage=LTO-4_SD" would have worked also but I am not sure
    how I would have ejected the full tape out.

</pre>
<hr />
Source for some of the data [here:](https://workaround.org/bacula-cheatsheet/)
<hr />
<br /> https://www.bacula-web.org/docs/install/selinux/

For Fedora users running SELinux, and using a local path to backup or restore, you will
have to set the correct SELinux context label:
To see the current context label for a directory that you plan to use type:<br />
	<span style="color: #3366ff;">ls -alZ /Full/Path</span>

Delete the current context (can use double-quotes in the full path section):<br />
	<span style="color: #3366ff;">semanage fcontext -d -t Old_Context_Type '/Full/Path(/.*)?'</span>

Add a new bacula friendly context (can use double-quotes in the full path section):<br />
<span style="color: #3366ff;">
semanage fcontext -a -t bacula_store_t '/Full/Path(/.*)?'<br />
restorecon -R -v /Full/Path</span>

Make sure bacula has ownership of the path <span style="color: #3366ff;">chown -R bacula:bacula /Full/Path</span>

