# python-script-for-downloading-fastq-sequences.
# The script downloads SRA files using the NCBI SRA toolkit.
# It is designed for linux based system like Ubuntu.
# The script requires the NCBI SRA toolkit to be already installed.
# In order to run this code you must have ncbi sra toolkit downloaded on your system.
# The script needs to be run within the SRA toolkit's bin directory, where the necessary tools reside.


#code
import subprocess
import os

# Specify the path to the SRA Toolkit binaries
sra_bin_path = "/home/msc2_11/sratoolkit.3.0.10-ubuntu64/bin"

# Add the path to the system PATH
os.environ["PATH"] = f"{sra_bin_path}:{os.environ['PATH']}"

# assign SRA IDS
sra_numbers = ["SRR19969232", "SRR19969233", "SRR19969234", "SRR19969235", "SRR19969236", "SRR19969237","SRR19969238"]

# Download .sra files
for sra_id in sra_numbers:
    print("Currently downloading: " + sra_id)
    prefetch = f"{sra_bin_path}/prefetch {sra_id}"
    print("The command used was: " + prefetch)
    subprocess.call(prefetch, shell=True)

# Extract .sra files into a folder named 'fastq'
for sra_id in sra_numbers:
    print("Generating fastq for: " + sra_id)
    fastq_dump = f"{sra_bin_path}/fastq-dump --outdir fastq --gzip --skip-technical --readids --read-filter pass --dumpbase --split-3 --clip {sra_id}"
    print("The command used was: " + fastq_dump)
    subprocess.call(fastq_dump, shell=True)


