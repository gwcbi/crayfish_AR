## Step 3: Aligning data using MAFFT 

1. Read and review MAFFT [documentation](https://mafft.cbrc.jp/alignment/software/manual/manual.html). We will be using the command line to execute MAFFT and will need to use a handful of the command options from the documentation.

> Reflection:
> 
> Why are we deciding to use local alignment instead of global alignment?

2. Create a slurm script, which contains the mafft command, titled `mafft.sh`. This slurm script will be submitted on pegasus.

You can either create this script on the terminal by doing:

A. `touch mafft.sh` - this creates a file <br/>
B. `nano mafft.sh` - this opens the file to edit within the terminal <br/>
C. Then you can paste the code below into the file. 

Alternatively, you can open a next text file in your text editor and save the file. Then upload to pegasus.

`mafft.sh`:

```bash
#!/bin/bash
#SBATCH -N 1
#SBATCH -t 2:00:00
#SBATCH -p tiny,short,defq
#SBATCH -o mafft.out
#SBATCH -e mafft.err

#--- Start the timer
t1=$(date +"%s")

mafft --op 3.00 --thread $(nproc) --localpair --maxiterate 1000 concatenated_crayfish.fasta > aligned_crayfish.fasta

#---Complete job
t2=$(date +"%s")
diff=$(($t2-$t1))
echo "[---$SN---] ($(date)) $(($diff / 60)) minutes and $(($diff % 60)) seconds elapsed."
echo "[---$SN---] ($(date)) $SN COMPLETE."

```

> Reflection:
> 
> What do all the lines in the above code block mean? Why are the options important to give to the slurm scheduler?

3. Submitting the script to slurm. <br/>

After creating the above script, we now have to send it off to the scheduler on pegasus. The way you do that is: `sbatch mafft.sh`

To monitor your script: `squeue`

4. Record all your methods in the manuscript. 

5. View the alignment in Geneious or online alignment viewers. How does it look? Do we need to adjust the commands or do we need to trim the alignment?