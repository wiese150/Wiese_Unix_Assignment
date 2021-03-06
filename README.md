# Wiese_Unix_Assignment
Repository for Unix Assignment

## Initial Process for Data Inspection
1.  Initial process is primarily just setting things up.  Initializing the repository, connecting to the remote, and getting this README prepared while making this note.
2.  Copied necessary data files and transpose program to repository.
3.  Now, inspecting the files.  The simplest way to start, in my view, is to use wc to view number of lines, words, and bytes.

fang_et_al_genotypes.txt posseses 2783 lines, 2744038 words, and 11054722 bytes from wc.  snp_position.txt possesses 984 lines, 13198 words, and 83747 bytes.

Both of these are, while not necessarily gigantic, a bit large for us to read using cat.

We can also use du on these files, with -h to make them more easily readable, in order to determine the file size, though wc has allowed us to do that already.  Still, du -h tells us that fang_et_al_genotypes.txt is 11 megabytes in size, and snp_position.txt is 84 kilobytes.  Again, not new information, but helpful to demonstrate the command.

4.  At this point, it's a good idea to get the number of columns with awk. For fang_et_al_genotypes.txt, this is 986.  snp_positions.txt has only 15 columns.

Neither seems to have a header, so this looks to be accurate throughout.

5.  Examine using head, while using cut to remove excess columns.  This at least gives an idea of what sort of things the files contain.

## Data Processing
1.  First step is to create distinct maize and teosinate genotype files.  For maize, grep -E "ZMMIL|ZMMLR|ZMMMR" fang_et_al_genotypes.txt > maize_genotypes.txt should do the trick.  Teosinate uses ZMPBA|ZMPIL|ZMPJA.  These were added to the header from the original genotypes file (created itself in a separate file) using cat to create the final file for transposition.

2.  Run transpose.awk on the maize and teosinte maize files, transferring the transposed data to new files.  Will need to then remove the first three lines of header from each using tail -n +4.

3.  Sort (sort -k1,1) the transposed files by the first column, as well as removing the header from and sorting snp_positions by snp_id.  Then cut out all columns from the sorted snp_positions file except for the first, third, and fourth - snp_id, chromosome, and position, respectively.

4.  Join (join -1 1 -2 1 -t $'\t' filename1 filename2) the sorted transposed maize file with the cut snp positions file to create a maize dataset file, and do the same with the sorted transposed teosinate file with the cut snp positions file to create a teosinate data file.  This took me a little bit, because I didn't realize that I'd forgotten to force the join command to separate by tab instead of whitespace.

5.  Create the individual chromosome files.  Start with the forward (increasing position) ones.  All it takes is a simple awk '$2 == n' filename.txt to select for the specific chromosomes, then sort based on number in the third column.  Then did the reverse (decreasing position value) ones in the same way.  After creating the decreasing position value files, used sed -i 's/?/-/g' filename to replace all instances of '?' in those with '-'.  After this, used grep to search for 'unknown' or 'multiple' in the maize and teosinte full data set files, and then create files containing only snps with unknown or multiple positions.

6.  Finish updating readme and post.
