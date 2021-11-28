Running the commands in pachctl

After connecting the to the pachctl and creating the repo we can list it using pchctl list repo


ricjha@docker-ubuntu-1-vm:~$ pachctl list repo
NAME                 CREATED     SIZE (MASTER) ACCESS LEVEL
push-answers-to-sql  3 hours ago 3.235KiB      OWNER        Output repo for pipeline push-answers-to-sql.
question_answer      3 hours ago 3.235KiB      OWNER        Output repo for pipeline question_answer.
question_answer_tick 3 hours ago 0B            OWNER        Cron tick repo for pipeline question_answer.


After that we can create the pipeline using the pachctl create pipeline -f pipeline1_spec.json command

We can view the pipeline created using the following command: pachctl list pipeline -f pipeline1_spec.json

pachctl list pipeline
ricjha@docker-ubuntu-1-vm:~$ pachctl list pipeline
NAME                VERSION INPUT             CREATED        STATE / LAST JOB   DESCRIPTION
push-answers-to-postgre 1       question_answer:/ 6 seconds ago  running / starting A pipeline that pushes answers to the database
question_answer     1       tick:@every 300s  11 seconds ago running / starting A pipeline that dowloads files from GCS and answers questions.

We can then view the logs using the following command: pachctl logs -v -j

ricjha@docker-ubuntu-1-vm:~$ pachctl logs -v -j 5d2c5ec96cf34c8fa02f47b84516e23e
[0000]  INFO parsed scheme: "dns" source=etcd/grpc
[0000]  INFO ccResolverWrapper: sending update to cc: {​​​​​​​[{​​​​​​​35.185.199.42:31400  <nil> 0 <nil>}​​​​​​​] <nil> <nil>}​​​​​​​ source=etcd/grpc
[0000]  INFO ClientConn switching balancer to "pick_first" source=etcd/grpc
2021-06-13 02:20:06.993141: I tensorflow/core/platform/cpu_feature_guard.cc:142] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
2021-06-13 02:20:07.029095: W tensorflow/python/util/util.cc:348] Sets are not currently considered sequences, but this may change in the future, so consider avoiding using them.
2021-11-18 02:20:07.100361: W tensorflow/core/framework/cpu_allocator_impl.cc:80] Allocation of 93763584 exceeds 10% of free system memory.
2021-11-18 02:20:07.349987: W tensorflow/core/framework/cpu_allocator_impl.cc:80] Allocation of 93763584 exceeds 10% of free system memory.
2021-11-18 02:20:07.382704: W tensorflow/core/framework/cpu_allocator_impl.cc:80] Allocation of 93763584 exceeds 10% of free system memory.
2021-11-18 02:20:08.516193: W tensorflow/core/framework/cpu_allocator_impl.cc:80] Allocation of 93763584 exceeds 10% of free system memory.
2021-11-18 02:20:08.618882: W tensorflow/core/framework/cpu_allocator_impl.cc:80] Allocation of 93763584 exceeds 10% of free system memory.
All model checkpoint layers were used when initializing TFDistilBertForQuestionAnswering.


All the layers of TFDistilBertForQuestionAnswering were initialized from the model checkpoint at distilbert-base-uncased-distilled-squad.
If your task is similar to the task the model of the checkpoint was trained on, you can already use TFDistilBertForQuestionAnswering for predictions without further training.
Downloading Files
Inside the File List Loop
Blob Created
File Downloaded as string
Calling the Question Answer Function
file_read
file_aded to intmd
writing file to location
question_answer completed
calling delete function
delete completed
