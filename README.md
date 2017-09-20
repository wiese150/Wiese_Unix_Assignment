# Wiese_Unix_Assignment
Repository for Unix Assignment

## Initial Process for Data Inspection
1.  Initial process is primarily just setting things up.  Initializing the repository, connecting to the remote, and getting this README prepared while making this note.
2.  Copied necessary data files and transpose program to repository.
3.  Now, inspecting the files.  The simplest way to start, in my view, is to use wc to view number of lines, words, and bytes.

fang_et_al_genotypes.txt posseses 2783 lines, 2744038 words, and 11054722 bytes from wc.  snp_position.txt possesses 984 lines, 13198 words, and 83747 bytes.

Both of these are, while not necessarily gigantic, a bit large for us to read using cat.

We can also use du on these files, with -h to make them more easily readable, in order to determine the file size, though wc has allowed us to do that already.  Still, du -h tells us that fang_et_al_genotypes.txt is 11 megabytes in size, and snp_position.txt is 84 kilobytes.  Again, not new information, but helpful to demonstrate the command.
