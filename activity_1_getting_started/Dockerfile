# wrench is the name of the 'wrench' docker image which was created with the base dockerfile in the root directory
FROM wrenchproject/wrench-pedagogic-modules:wrench-1.0 

USER root

WORKDIR /home/wrench/

# pull pedagogic-modules, go to desired activity, checkout gh-pages for "published" version, build
RUN git clone https://github.com/wrench-project/wrench-pedagogic-modules.git \
    && cd wrench-pedagogic-modules/activity_1_getting_started \
    && git checkout master\
    && cmake -DCMAKE_CXX_FLAGS="-DREMOTE_STORAGE" . && make clean && make && mv ./activity_simulator ./simulator_remote_storage 
    
RUN chown -R wrench ./wrench-pedagogic-modules

USER wrench
WORKDIR /home/wrench/wrench-pedagogic-modules/activity_1_getting_started

CMD ./simulator_remote_storage platform_files/platform.xml workflow_files/workflow.dax \
         --log="root.fmt:[%d][%h:%t]%e%m%n" \
         --log=root.thresh:critical \
         --log=wms.thresh:debug \
         --log=simple_wms.thresh:debug \ 
         --log=simple_wms_scheduler.thresh:debug

