# ACM DEBS Grand Challenge tutorial system

It is able to  pass DEBSParrotBenchmark. In order to do that it receives messages on `inputQueue` and sends all of them
except `TERMINATION_MESSAGE` to `outputQueue`. Receiving of the `TERMINATION_MESSAGE` on `inputQueue`
means no more followed messages. After the system has processed all the messages it must send `TERMINATION_MESSAGE` to
`outputQueue`.
