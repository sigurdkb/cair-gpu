FROM nvidia/cuda:9.1-cudnn7-devel-ubuntu16.04
ARG SRC=rsync://172.17.0.1/MathWorks/
ARG FIK

# Update the repository, install packages and clean
RUN apt-get update && apt-get install -y \
    libx11-6 \
    libxext6 \
    libxrandr2 \
    libxt6 \
    emacs \
    nano \
    vim \
    meld \
    rsync \
    && rm -rf /var/lib/apt/lists/*

# Copy installer answer file and license file
COPY MathWorks /MathWorks


# Get and install matlab
RUN rsync -aP $SRC /MathWorks \
    && echo "fileInstallationKey=$FIK" >> /MathWorks/installer_input.txt \
    && /MathWorks/R2018a/install -mode silent -inputFile /MathWorks/installer_input.txt \
    && ln -s /usr/local/R2018a/bin/matlab /usr/bin/matlab \
    && echo "alias matlab='matlab -nodisplay -nosplash'" > ~/.bash_aliases \
    && rm -fdr /MathWorks*
