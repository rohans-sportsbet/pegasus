# run PEGASUS 

pip install -e pegasus

pip install -Iv tensorflow-datasets==3.0.0

pip install -Iv tfds-nightly==3.1.0.dev202006230105 


# run pegasus evaluation

python3 pegasus/bin/evaluate.py --params=cnn_dailymail_transformer --param_overrides=vocab_filename=ckpt/pegasus_ckpt/c4.unigram.newline.10pct.96000.model,batch_size=1,beam_size=8,beam_alpha=0.8 --model_dir=ckpt/pegasus_ckpt/cnn_dailymail/model.ckpt-210000 --evaluate_test

python3 pegasus/bin/evaluate.py --params=racing_transformer --param_overrides=vocab_filename=ckpt/pegasus_ckpt/c4.unigram.newline.10pct.96000.model,batch_size=1,beam_size=8,beam_alpha=0.8 --model_dir=ckpt/pegasus_ckpt/cnn_dailymail/model.ckpt-210000 --evaluate_test

_run_short_racing_transformer:

python3 pegasus/bin/evaluate.py --params=racing_transformer --param_overrides=vocab_filename=ckpt/pegasus_ckpt/c4.unigram.newline.10pct.96000.model,batch_size=1,beam_size=5,beam_alpha=0.6 --model_dir=ckpt/pegasus_ckpt/racing  --evaluate_test

_run_long_racing_transformer:

python3 pegasus/bin/evaluate.py --params=long_racing_transformer --param_overrides=vocab_filename=ckpt/pegasus_ckpt/c4.unigram.newline.10pct.96000.model,batch_size=1,beam_size=5,beam_alpha=0.6 --model_dir=ckpt/pegasus_ckpt/racing_long  --evaluate_test

# run pegasus fine-tuning with your own racing material

python3 pegasus/bin/train.py --params=racing_transformer \
--param_overrides=vocab_filename=ckpt/pegasus_ckpt/c4.unigram.newline.10pct.96000.model \
--train_init_checkpoint=ckpt/pegasus_ckpt/model.ckpt-1500000 \
--model_dir=ckpt/pegasus_ckpt/racing

python3 pegasus/bin/train.py --params=racing_transformer \
--param_overrides=vocab_filename=ckpt/pegasus_ckpt/c4.unigram.newline.10pct.96000.model \
--train_init_checkpoint=ckpt/pegasus_ckpt/cnn_dailymail/model.ckpt-210000 \
--model_dir=ckpt/pegasus_ckpt/racing

_train_short_racing_transformer:

python3 pegasus/bin/train.py --params=racing_transformer \
--param_overrides=vocab_filename=ckpt/pegasus_ckpt/c4.unigram.newline.10pct.96000.model \
--train_init_checkpoint=ckpt/pegasus_ckpt/racing/model.ckpt-10000 \
--model_dir=ckpt/pegasus_ckpt/racing

_train_long_racing_transformer:

python3 pegasus/bin/train.py --params=long_racing_transformer \
--param_overrides=vocab_filename=ckpt/pegasus_ckpt/c4.unigram.newline.10pct.96000.model \
--train_init_checkpoint=ckpt/pegasus_ckpt/cnn_dailymail/model.ckpt-210000 \
--model_dir=ckpt/pegasus_ckpt/racing_long

# run interactive summary

python3 pegasus/bin/interactive_summary.py --model=racing --param_overrides=vocab_filename=ckpt/pegasus_ckpt/c4.unigram.newline.10pct.96000.model,batch_size=1,beam_size=5,beam_alpha=0.6 --input="Ballarat Turf Club is situated at the Dowling Forest Racecourse, 113km west of Melbourne and houses races from 1,000m through to steeple racing at 3,400m. The race course consists of an old and a new track and not only is the home of Ballarat races but the Race Club also caters for 300 horses in training. Capacity field is 18 runners and with a straight of 450m inside barriers can be an advantage for several distances between 1,400 to 2,200m. The main race day is the Ballarat Cup which attracts around 17,000 people and occurs in November. The club also hosts a number of other popular events with highlights in March and July. 113kms west of Melbourne lies the Ballarat Racecourse on the site known as the Dowling Forest. And is only 15kms north-west of Ballarat. This Dowling Forest complex is situated on 300 hectares of land in the locality of Miner's rest. With a home straight 450m long and an overall circumference of 1900m, The Ballarat Racecourse holds a wide variety of races ranging from 1000m sprints right up to 3,400m steeple races. Apart from races, the course is renowned for being one of the best training facilities in Victoria. The course facilities are spectator friendly and offer plenty of open space for patrons. The track itself is a spacious 30m wide. November sees the Ballarat Racecourse hold its premier event, the 2200m Ballarat Cup which is the final feature event in the Victorian Spring Racing Carnival.TL;DR:"


# git
pegasus branch: racing