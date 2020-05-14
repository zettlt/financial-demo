## greet/bye path
* greet: hi
    - utter_greet
* goodbye: bye
    - utter_goodbye

## say goodbye
* goodbye: bye
    - utter_goodbye

## pay credit card happy path
* greet: hi
    - utter_greet
* pay_cc: i want to pay off my [gringots](credit_card) credit card
    - cc_payment_form
    - form{"name":"cc_payment_form"}
* form: inform: my [current balance](payment_amount)
    - form: cc_payment_form
* form: inform: [next week tuesday
    - form: cc_payment_form
* form: affirm: /affirm
    - form: cc_payment_form
    - form{"name":null}

## pay credit card and check account balance inside form
* pay_cc: i want to pay off my [justice bank](credit_card) credit card
    - cc_payment_form
    - form{"name":"cc_payment_form"}
* form: inform: my [current balance](payment_amount)
    - form: cc_payment_form
* check_balance: what's my account balance?
    - action_account_balance
    - utter_ask_continue
* affirm: Yes
    - cc_payment_form
* form: inform: 8am on Friday February 21 2020
    - form: cc_payment_form
* form: affirm: /affirm
    - form: cc_payment_form
    - form{"name":null}

## transfer money
* transfer_money: I want to transfer money to [John](PERSON)
    - transfer_form
    - form{"name":"transfer_form"}
* form: inform: [$60](amount-of-money:60)
    - form: transfer_form
* form: affirm: /affirm
    - form: transfer_form
    - form{"name":null}

## is there a transfer charge
* ask_transfer_charge: is there a transfer charge
    - utter_transfer_charge

## transfer money
* transfer_money: i want to transfer money to [Percy](PERSON)
    - transfer_form
    - form{"name":"transfer_form"}
* ask_transfer_charge: is there a transfer charge?
    - utter_transfer_charge
    - transfer_form
* form: inform: [600](number)
    - form: transfer_form
* form: affirm: /affirm
    - form: transfer_form
    - form{"name":null}

## search transactions happy path
* search_transactions: I want to search my spending history
    - transact_search_form
    - form{"name":"transact_search_form"}
* form: inform: Jan 2019
    - form: transact_search_form
    - form{"name":null}
* thankyou: thank you
    - utter_noworries

## search transactions happy path no greet or thanks
* check_earnings: how much did I earn in Jan 2019?
    - transact_search_form
    - form{"name":"transact_search_form"}
    - form{"name":null}

## search transactions switch to transfer money, deny
* check_earnings: how much did i earn?
    - transact_search_form
    - form{"name":"transact_search_form"}
* transfer_money: actually I want to transfer money
    - utter_ask_switch_goal
* deny: no
    - transact_search_form
* form: inform: january 2020
    - form: transact_search_form
    - form{"name":null}

## search transactions switch to transfer money, don't continue transactions
* check_earnings: How much did i earn
    - transact_search_form
    - form{"name":"transact_search_form"}
* transfer_money: i want to transfer money
    - utter_ask_switch_goal
* affirm: yes
    - transfer_form
    - form{"name":"transfer_form"}
* form: inform: to [Paul](PERSON)
    - form: transfer_form
* form: inform: [$45](amount-of-money:45)
    - form: transfer_form
* form: affirm: /affirm
    - form: transfer_form
    - form{"name":null}
    - utter_ask_back_to_transact
* deny: no
    - utter_ok

## search transactions switch to transfer money
* search_transactions: I want to search my spending history
    - transact_search_form
    - form{"name":"transact_search_form"}
* transfer_money: actually I want to transfer money to [Lisa](PERSON)
    - utter_ask_switch_goal
* affirm: yes
    - transfer_form
    - form{"name":"transfer_form"}
* form: inform: [$35](amount-of-money:35)
    - form: transfer_form
* form: affirm: /affirm
    - form: transfer_form
    - form{"name":null}
    - utter_ask_back_to_transact
* affirm: yes
    - transact_search_form
    - form{"name":"transact_search_form"}
* form: inform: january 2020
    - form: transact_search_form
    - form{"name":null}

## New Story

* greet: hi
    - utter_greet
* goodbye: bye
    - utter_goodbye

## Story from conversation with 1200800076 on May 14th 2020

* start: /start
* hi: hi
* hiu: /hiu
* greet: hi
    - utter_greet
* check_balance: what is my balance
    - action_account_balance
    - slot{"payment_amount":null}
* pay_cc: i want to pay my credit card
    - cc_payment_form
    - form{"name":"cc_payment_form"}
    - slot{"requested_slot":"credit_card"}
* inform: [gringots](credit_card)
    - slot{"credit_card":"gringots"}
    - cc_payment_form
    - slot{"credit_card":"gringots"}
    - slot{"requested_slot":"payment_amount"}
* inform: [1200](number)
    - cc_payment_form
    - slot{"payment_amount":1200}
    - slot{"amount_of_money":"1200.00"}
    - slot{"currency":"$"}
    - slot{"requested_slot":"time"}
* inform: [2020-05-15T00:00:00.000-07:00](time)
    - slot{"time":"2020-05-15T00:00:00.000-07:00"}
    - cc_payment_form
    - slot{"time":"Friday May 15, 2020"}
    - slot{"grain":"day"}
    - slot{"requested_slot":"confirm"}
* affirm: /affirm
    - cc_payment_form
    - slot{"confirm":true}
    - slot{"credit_card":null}
    - slot{"payment_amount":null}
    - slot{"confirm":null}
    - slot{"time":null}
    - slot{"grain":null}
    - form{"name":null}
    - slot{"requested_slot":null}
* thankyou: thank
    - utter_noworries
