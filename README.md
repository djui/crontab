<h1>Crontab</h1>

=====================

__Authors:__ Bjorn Jensen-Urstad ([`bjorn.jensen.urstad@gmail.com`](mailto:bjorn.jensen.urstad@gmail.com)).

Crontab for Erlang.


Execute scheduled functions.

API is consists of scheduler:add/3 and scheduler:remove/1.

<pre>
  crontab:add(Name::atom(), Spec::list(), MFA::mfa()) -> ok | {error, Rsn}
  crontab:remove(Name::atom()) -> ok | {error, Rsn}

  Spec = [year(), month(), day(), hour(), min()]

  year()  :: 0..N  | '*' | [2013, 2015, ..]
  month() :: 1..12 | '*' | [1, 2, 3, ..]
  day()   :: 1..31 | monday | tuesday | wednesday | thursday | friday |
             saturday | sunday | [monday, 21, friday, ..]
  hour()  :: 0..23 | '*' | [12, 22, ..]
  min()   :: 0..59 | '*' | [0, 15, 30, 45, ..]

  MFA = {module, function, args}
</pre>


Example usage:
<pre>
  ok = application:start(crontab),
  MFA = {module, function, []},

  %% once/week, monday 8.30
  ok = crontab:add(foo, ['*', '*', monday,  8, 30], MFA),
  %% first day of month, 00.00
  ok = crontab:add(bar, ['*', '*', 1, 0, 0], MFA),
  %% 29th of february, 20.00
  ok = crontab:add(baz, ['*', 2, 29, 20, 0], MFA),
  %% every 15 minute on mondays and fridays
  ok = crontab:add(buz, ['*', '*', [monday, friday], '*', [0, 15, 30, 45]], MFA),
  ok = application:stop(crontab),
</pre>


* Manifest
* eof
