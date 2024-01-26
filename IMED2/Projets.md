**Dernière séance : soutenances de projet**
14/02

## Presentation
blablabla
### SSVEP

Steady-State Visually Evoked Potentials (SSVEP) is an example of a paradigm where elements flicker steadily on a screen, but with different frequencies. When the user focuses on a specific element, the corresponding frequency can become stronger in the EEG originating from the occipital lobe. For SSVEP, machine learning can be used to learn classifiers that distinguish between the flickering frequencies. There are also novel approaches requiring no classifier training, but presently we are not providing such approaches in OpenViBE.

- Pros: User does not need skill. SSVEP is less sensitive to time precision than P300.
- Cons: The flicker may quickly fatigue the user. It may be difficult to reliably select between more than 3 elements.
- Electrodes: Around and including OZ.
- Usual pace: One prediction each few seconds of signal. Can be used to mimic continuous control (sliding window).

OpenViBE is shipped with two simple demo games based on SSVEP: the SSVEP Demo and the Mind Shooter. Both games involve controlling a spaceship and shooting at targets.
