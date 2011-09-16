## A JRuby wrapper to the JGroups toolkit

[JGroups](http://www.jgroups.org) is toolkit that allows reliable
multicast communication.

This wrapper will be attempt to expose some of the basic but hopefully
useful parts of the API in a ruby fashion. Starting with the ability to
send messages to the cluster. 

Watch out for network configuration errors. If you see errors stating
that the network is down, then you likely don't have multicasting 
setup correctly on network, or you are on a WIFI network. See the
[JGroups site](http://www.jgroups.org/tutorial/html/ch01.html#d0e142)
for information on how to run without a network.

Let's see some code:
    
    # connect to the multicast cluster
    RGroups::Channel.connect 'MyCluster' do

      # set a callback to receive messages
      receiver do |message|
        puts "#{message.source}: #{message}"
      end


      # sending a message
      send_message('Howdy')
      send_message('Hi', {:source => '192.168.1.1', 
                          :destination => '192.168.1.100'})

      # you can actually send any java object
      send_message([1,2,3].to_java)

      # Don't forget to handle it on receive
      # message.data.to_a
    end


Check the examples to see an application using the library
 
    # run an example
    jruby --1.9 examples/rchat_test.rb


Features I'd like to add:

  * More examples
  * use JGroups shared state facilities

