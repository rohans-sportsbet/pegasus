# run PEGASUS 

pip install -e pegasus
pip install -Iv tensorflow-datasets==3.0.0
pip install -Iv tfds-nightly==3.1.0.dev202006230105 


# run pegasus evaluation

python3 pegasus/bin/evaluate.py --params=cnn_dailymail_transformer --param_overrides=vocab_filename=ckpt/pegasus_ckpt/c4.unigram.newline.10pct.96000.model,batch_size=1,beam_size=8,beam_alpha=0.8 --model_dir=ckpt/pegasus_ckpt/cnn_dailymail/model.ckpt-210000 --evaluate_test

python3 pegasus/bin/evaluate.py --params=racing_transformer --param_overrides=vocab_filename=ckpt/pegasus_ckpt/c4.unigram.newline.10pct.96000.model,batch_size=1,beam_size=8,beam_alpha=0.8 --model_dir=ckpt/pegasus_ckpt/cnn_dailymail/model.ckpt-210000 --evaluate_test

python3 pegasus/bin/evaluate.py --params=racing_transformer --param_overrides=vocab_filename=ckpt/pegasus_ckpt/c4.unigram.newline.10pct.96000.model,batch_size=1,beam_size=5,beam_alpha=0.6 --model_dir=ckpt/pegasus_ckpt/racing_cnn  --evaluate_test


# run pegasus fine-tuning with your own racing material

python3 pegasus/bin/train.py --params=racing_transformer \
--param_overrides=vocab_filename=ckpt/pegasus_ckpt/c4.unigram.newline.10pct.96000.model \
--train_init_checkpoint=ckpt/pegasus_ckpt/model.ckpt-1500000 \
--model_dir=ckpt/pegasus_ckpt/racing

python3 pegasus/bin/train.py --params=racing_transformer \
--param_overrides=vocab_filename=ckpt/pegasus_ckpt/c4.unigram.newline.10pct.96000.model \
--train_init_checkpoint=ckpt/pegasus_ckpt/cnn_dailymail/model.ckpt-210000 \
--model_dir=ckpt/pegasus_ckpt/racing

python3 pegasus/bin/train.py --params=racing_transformer \
--param_overrides=vocab_filename=ckpt/pegasus_ckpt/c4.unigram.newline.10pct.96000.model \
--train_init_checkpoint=ckpt/pegasus_ckpt/racing_cnn/model.ckpt-10000 \
--model_dir=ckpt/pegasus_ckpt/racing


# run interactive summary

python3 pegasus/bin/interactive_summary.py --model=racing --param_overrides=vocab_filename=ckpt/pegasus_ckpt/c4.unigram.newline.10pct.96000.model,batch_size=1,beam_size=5,beam_alpha=0.6 --input=""


# git
pegasus branch: racing