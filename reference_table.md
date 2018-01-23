| command | description 			   							 | example 					  	  	 		      |
|---------|------------------------------------------------------|------------------------------------------------|
| pwd     | print working directory    		 					 | pwd						      	 		      |
| ls	  | list contents of directory 		 					 | ls 						      	  		      |
| cd 	  | change directory		   		 					 | cd ~/Documents 		 	      	 		      |
| mkdir	  | make directory			   		 					 | mkdir pen      		  					      |
| ssh	  | log into a remote server   	     					 | ssh <pen>@<apple_pen>.com 				      |
| mv	  | move something to a new location 					 | mv apple apple_pen 						      |
| rmdir	  | remove a directory									 | rmdir apple_pen 	 	 						  |
| rm   	  | more general 'remove' command, including files 		 | rm apple_pen.txt 							  |
| wget	  | download something from a URL						 | wget [www.pen.com/pineapple/pineapple_pen.txt](https://media.giphy.com/media/10fVn57KfQ8Wkw/giphy.gif) |
| cat	  | print contents of a file to screen					 | cat pineapple_pen.txt 					      |
| gzip 	  | a tool for dealing with gzip files					 | gzip pineapple_pen.txt 					      |
| zcat	  | print contents of a gzipped file to screen			 | zcat pineapple_pen.txt.gz 				      |
| whatis  | get a short description of a program				 | whatis zcat 								      |
| man	  | print the man(ual) page of a command 				 | man zcat									      |
| head 	  | print first X number of lines of a file to screen	 | head -n 20 pineapple_pen.txt 	  		      |
| &#124;  | pipe, a way to pass output of one command to another | cat pineapple_pen.txt &#124; head 		      |
| tail 	  | print last X number of lines of a file to screen	 | tail -n 20 pineapple_pen.txt 			      |
| less 	  | print file to screen, but allow scrolling			 | less pineapple_pen.txt 					      |
| wc	  | tool to count words, lines or bytes of a files 		 | wc -l pineapple_pen.txt 					      |
| grep	  | print to screen lines in a file matching a pattern 	 | grep pineapple_pen.txt &#124; grep apple       |
| ln 	  | make a (sym)link between a file and a new location   | ln -s pineapple_pen.txt apple_pen.txt 		  |
| nano 	  | user-friendly terminal-based text editor			 | nano apple_pen.txt 							  |
| $VAR 	  | Dollar sign + text indicates the name of a variable  | $APPLE=pen 									  |
| echo	  | prints string to screen								 | echo $APPLE 									  |
| for     | begins 'for' loop, requires 'in', 'do' and 'done'	 | for * in apple pen; do cat apple_pen.txt; done |

TODO: Re-order for bette rflow and fix examples