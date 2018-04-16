FROM nvcr.io/nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04

# Update the repository, install packages and clean
RUN apt-get update && apt-get install -y \
    libx11-6 \
    libxext6 \
    libxrandr2 \
    libxt6 \
    emacs \
    meld \
    p7zip-full \
    && rm -rf /var/lib/apt/lists/*

# Copy installer answer file and license file
COPY MathWorks /MathWorks

# Get install files
RUN wget http://thor.uia.no:8080/MathWorks.7z \
    && 7z x MathWorks.7z \
    && /MathWorks/R2017b/install -mode silent -inputFile /MathWorks/installer_input.txt \
    && rm -fdr /MathWorks*
