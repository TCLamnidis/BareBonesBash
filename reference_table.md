| command | description 			   							 | example 					  	  	 		      			  | common flags or arguments	   |
|---------|------------------------------------------------------|------------------------------------------------------------|--------------------------------|
| pwd     | print working directory    		 					 | pwd						      	 		      			  |								   |
| ls	  | list contents of directory 		 					 | ls 						      	  		      			  | -l (long info)				   |
| mkdir	  | make directory			   		 					 | mkdir pen      			  				      			  |								   |
| cd 	  | change directory		   		 					 | cd ~/pen 		 	      	 			      			  | ~ (home dir), - (previous dir) |
| ssh	  | log into a remote server   	     					 | ssh <pen>@<apple>.com 					      			  | -x (allows graphical windows)  |
| mv	  | move something to a new location (& rename if needed)| mv pen pineapple 						      			  |								   |
| rmdir	  | remove a directory									 | rmdir pineapple		 	 					  			  |								   |
| wget	  | download something from a URL						 | wget [www.pineapple.com/pen.txt](https://media.giphy.com/media/10fVn57KfQ8Wkw/giphy.gif) | -i (use input file) |
| cat	  | print contents of a file to screen					 | cat pen.txt 				  								  |								   |
| gzip 	  | a tool for dealing with gzip files					 | gzip pen.txt 					      					  | -l (show info)				   |
| zcat	  | print contents of a gzipped file to screen			 | zcat pen.txt.gz 				      						  |								   |
| whatis  | get a short description of a program				 | whatis zcat 								      			  |								   |
| man	  | print the man(ual) page of a command 				 | man zcat									      			  |								   |
| head 	  | print first X number of lines of a file to screen	 | head -n 20 pineapple.txt 	  		      				  | -n (number of lines to show)   |
| &#124;  | pipe, a way to pass output of one command to another | cat pineapple.txt &#124; head 		      				  |								   |
| tail 	  | print last X number of lines of a file to screen	 | tail -n 20 pineapple.txt 			      				  | -n (number of lines to show)   |
| less 	  | print file to screen, but allow scrolling			 | less pineapple.txt 					      				  |								   |
| wc	  | tool to count words, lines or bytes of a files 		 | wc -l pineapple.txt 					      				  |	-l (number of lines not words) |
| grep	  | print to screen lines in a file matching a pattern 	 | grep pineapple.txt &#124; grep pen       				  |  							   |
| ln 	  | make a (sym)link between a file and a new location   | ln -s pineapple.txt pineapple_pen.txt 		 			  |	-s (make _symbolic_ link) 	   |
| nano 	  | user-friendly terminal-based text editor			 | nano pineapple_pen.txt 									  |								   |
| rm   	  | more general 'remove' command, including files 		 | rm pineapple_pen.txt 									  | -r (to remove directories)	   |
| $VAR 	  | Dollar sign + text indicates the name of a variable  | $PPAP=pen 												  |								   |
| echo	  | prints string to screen								 | echo $PPAP 												  |								   |
| for     | begins 'for' loop, requires 'in', 'do' and 'done'	 | for pineapple apple; do echo "$PPAP" pineapple apple $PPAP |								   |
