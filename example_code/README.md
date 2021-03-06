Get Started with Performance Tuning and Optimization 

Sample Matrix-Matrix multiplication code for Princeton Research Computing Bootcamp 2018

This is intended to use as a example to profile with performance tuning tools such as VTune. The code does not do anything useful and is for illustrative/educational use only. It is not meant to be exhaustive or demostrating optimal matrix-matrix multiplication techniques.

Instructions for Running on Adroit

1. Log into Adroit with X11 forwarding enabled
ssh -Y -C <username>@adroit.princeton.edu
2. Load environment modules
module load intel
module load intel-vtune
3. Build the example code and call executable "mm.out"
(What happens if you forget the -g?)
e.g. icpc -g -mkl -O3 -xhost matmul_test.cpp -o mm.out
Short test on head node: ./mm.out 250 (250x250 matrix)
4. Run the provided script to submit a VTune wrapped job to the scheduler
./submit_to_scheduler
This will, by default, run a 500x500 matrix example on a compute node using the VTune "Hotspots" analysis. When it finishes it will create a directory with the results named something like r000hs, where 000 is incremented by 1 for each new analysis.
5. Open the resulting directory with VTune GUI
e.g. amplxe-gui r000hs
6. Explore "Bottom-up" and "Top-down Tree" and double click on hotspots to look at line-by-line performance
Edit the file "submit.slurm" to increase the matrix size (originally 500) and rerun the analysis. WARNING: don't go over 1500!
7. Load environment module for Advisor
e.g. `module load intel-advisor`
8. Run the script to submit a Advisor wrapped job to the schedule with survey analysis
1) In ./submit.slurm, change the job execution command to advisor command line with survey analysis
2) Run `./submit_to_scheduler`
9. Open the resulting directory with Advisor
e.g., `advixe-gui <RESULT_DIR>`
10. Explore "Survey" report 
11. Run the script to submit a Advisor wrapped job to the schedule with tripcounts analysis
1) In ./submit.slurm, change the job execution command to advisor command line with tripcounts analysis
2) Run `./submit_to_scheduler`
12. Open the resulting directory with Advisor
e.g., `advixe-gui <RESULT_DIR>`
13. Explore "Tripcounts & Roofline" report 


