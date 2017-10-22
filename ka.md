#A Race Condition:
is when two thread on a multi threaded machine want to access the same data.

#mutal exclusion:
because then there is no other way to force the program to stop then turn off the machine.

#Petersons Solution
i.	Thread a (0) -> <enter_region> other = 1 loser = 0 interested = {true, false}
	Thread b (1) -> <enter_region> other = 0 loser = 1 interested = {true, true}
	b is blocked because 1(loser) == 1(process) && the other is enterested as well.
	a enters the region unblocked because now 1(loser) != 0(process) and after it, it unlock the b.

ii

	Thread a (turn should be 0)
	Thread b (turn should be 1)

	a enters the critical region and run until the turn = 1(so the was also executed) then the scheduler
	say the time for a is over (note: a has not left the critical region yet) so b starting and b is not blocked
	because a set the turn to 1 already.

iii.

	turn means which process should run right now and which not.


iv.

	while (True) {
		while (turn != 0) ;
			critical_region();
			turn = 1;
			noncritical_region();
	}
	while (True) {
		while (turn != 1) ;
			critical_region();
			turn = 2;
			noncritical_region();
	}
	while (True) {
		while (turn != 2) ;
			critical_region();
			turn = 0;
			noncritical_region();
	}





	int loser1, loser2 // shared variable
	Bool interested[2] // two processes only
	void enter_region(int process)
	{
		int other = 1 - process;
		interested[process] = True;
		loser1 = process;
		while (loser == process && interested[other]) ;
	}



	int loser1 = -1,loser2 = -1;
	Bool interested[3];
	void enter_region(int process)
	{
		int other1 = 2 - process;
		if(process == other1)
			other1 = 2;
		int other2 = 1 - process;
		if(other2 > 0)
			other2 = other2 * -1;
			//works until here


		if(loser1 == -1)
			loser1 == process;
		else if(loser2 == -1)
			loser2 == process;

		interested[process] = true;

		while((loser1 == process || loser2 == process) && (interested[other1] && interested[other2]));
	}
