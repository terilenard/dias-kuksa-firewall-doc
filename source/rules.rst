4. Rule language
================

The set of rules contained in the rule file are described using a Extensible Markup Language (XML) based language. 
A pattern is defined as an *action rule*, which ultimately is applied on every data frame. An *action rule* can be linked together with a sequence of *action rules* creating a *state-chain*. This describes actions that must be taken on a sequence of frames, thus providing contextual detection capabilities. Subsequently, each *action rule* provides the ability to generate a hierarchical expression, allowing definitions for deep packet inspection rules. This step leverages boolean operators, such as *AND* and *OR*, used to link together different expressions.
 
4.1 Terms and keywords
----------------------

1. **Rule file** : an XML file containing the definitions for the *rules*, *actions* as well as the way the rules are chained togheter creating the *rule-chains* and *state-chains*.
2. **Rule** : a pattern searched within an incoming CAN frame. Each rule is bound to an *action*, which in term triggers an event if a pattern is found.   
3. **Action** : the operation that must take place as a consequence to a specific event. An action can have one of the four values: PERMIT, DROP, PERMIT-LOG and DROP-LOG.
 a. *PERMIT* : the incomming frame should be allowed to pass.
 b. *DROP* : the frame shound not be further forwarded.
 c. *PERMIT-LOG* :  the incomming frame should be allowed to pass, additionaly the event should be logged by the Secure Logging unit.
 d. *DROP-LOG* : the frame shound not be further forwarded, additionaly the event should be logged by the Secure Logging unit.


.. code-block:: XML

      <!-- FIREWALL TEST RULE for CID: 124 (hex) -->
      <rule cid="292" id="test_frame_2" action="PERMIT">
      </rule>

      The above rule (FIREWALL) will PERMIT all frames with the CID 292 (124 in hex).

      <!-- IDS TEST RULE for CID: 123 (hex) -->
      <rule cid="291" id="test_frame" actrion="DROP">
        <payload>
          <expression>
            <operator type="AND">
              <byte index="0" value="1"/>
              <byte index="1" value-range="1..170"/>
            </operator>
          </expression>
        </payload>
      </rule>

    The above rule (IDS) will DROP all frames with the CID 291 (123 in hex) if the first byte from the payload
    has the value 1 and the second byte has a value in the range [1,170].

4.2 State chains
----------------

In the **state chains** the rules are chained together in sequences of rules, allowing the SFW/IDS to make decisions on a current frame, based on the past received traffic.
 
.. code-block:: XML

  <state-chains>
    <chain id="state-chain-1">
      <rule id="1-permit" action="PERMIT"/>
      <rule id="2-permit" action="PERMIT"/>
      <rule id="3-drop" action="DROP"/>
    </chain>
  </state-chains>

 In the above example a state chain is defined, containing 3 chained rules.
