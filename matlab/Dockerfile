FROM nvidia/cuda:9.1-cudnn7-devel-ubuntu16.04
ARG SRC
ARG FIK

# Update the repository, install packages and clean
RUN apt-get update && apt-get install -y \
    libx11-6 \
    libxext6 \
    libxrandr2 \
    libxt6 \
    emacs \
    meld \
    p7zip-full \
    wget \
    && rm -rf /var/lib/apt/lists/*

# Copy installer answer file and license file
COPY MathWorks /MathWorks


# Get install files
RUN wget $SRC \
    && 7z x MathWorks.7z \
    && echo "fileInstallationKey=$FIK" >> /MathWorks/installer_input.txt \
    && /MathWorks/R2018a/install -mode silent -inputFile /MathWorks/installer_input.txt \
    && rm -fdr /MathWorks*
