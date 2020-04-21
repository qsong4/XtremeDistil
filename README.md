README
--------------------------

Step 1: 

(a) Fine-tune BERT language model on transfer set (pre-train on unlabeled data starting from checkpoint: https://storage.googleapis.com/bert_models/2018_11_23/multi_cased_L-12_H-768_A-12.zip)

(b) Fine-tune BERT on the downstream task. 

Step 2: Run the distillation-code. E.g.: "python3.6 BERT_NER.py --task_name=NER --do_lower_case=False --crf=False --do_train=False --do_eval=False --do_predict=True --data_dir=../datasets/NER --vocab_file=../models/multi_cased_L-12_H-768_A-12/vocab.txt --bert_config_file=../models/multi_cased_L-12_H-768_A-12/bert_config.json --max_seq_length=32 --train_batch_size=32 --eval_batch_size=32 --predict_batch_size=32 --learning_rate=2e-5 --num_train_epochs=3.0 --output_dir=/tmp --init_checkpoint=../models/ner_ft_lm/model.ckpt-100000 --pred_file=../datasets/NER/transfer_set.tsv --model_dir=../models/multi_ner_unify --s1_loss=kld --s1_opt=adam --s2_opt=adam --path=.. --distil_task=NER --word_embedding_file=mbase.txt --teacher_layer=-7"

Arguments:
-- refer to code for argument description
-- init_checkpoint contains the model checkpoint from Step 1.a
-- pred_file is the unlabeled transfer set
-- model_dir contains the model checkpoint for fine-tuned classifier from Step 1.b
-- word_embedding_file (could be Glove or SVD on MBERT word embedding)
-- teacher_layer to distil froms

Sample data files and format in data directory