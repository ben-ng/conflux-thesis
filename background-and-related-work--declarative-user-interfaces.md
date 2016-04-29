# Declarative User Interfaces

User interfaces are traditionally built using imperative methods. For example, a `Button` object is initialized, after which its text is set using `myButton.setText("Submit")`. If the button has to enter a loading state, the programmer might call `myButton.setText("Loading...")` and `myButton.setDisabled(true)`. This approach does not scale well to complex user interfaces because it results in duplicative, spaghetti-like code.

Consider a simple user interface that consists of a text input and a button. The button should only be visible when the text input is not empty. If the button is clicked, it should enter the disabled state and change its text to indicate to the user that an action is in progress. The text input should also enter the disabled state after the button has been clicked.

	// Presentation, state, and logic are muddled in this
	// example of an imperatively constructed user interface
	
	class FormView extends View

	Button button
	TextInput input

	constructor FormView
		// Create instances of user interface elements
		this.button = new Button()
		this.input = new TextInput()
		this.isLoading = false

		// Set initial state of user interface elements
		this.button.setText("Submit")

		// Bind event listeners
		this.input.onChange = this.onInputChange
		this.button.onClick = this.onButtonClick

		this.view.addSubview(this.input)
		this.view.addSubview(this.button)

	function onInputChange
		if this.input.length > 0
			this.button.removeFromSuperview()
		else
			this.view.addSubview(this.button)

	function onButtonClick
		this.button.setText("Loading...")
		this.button.setDisabled(true)
		this.input.setDisabled(true)

	destructor ~FormView
		delete this.button
		delete this.input

This example illustrates how user interfaces are traditionally implemented. It is difficult to tell how the user interface behaves by reading the code, because the interface is mutated in various event handlers. As the complexity of the user interface grows it becomes incredibly difficult to understand what the current state of the user interface is. This leads to bugs that are difficult to track down, and encourages programmers to employ band-aid like fixes which contribute to technical debt.

Declarative user interfaces have come into vogue because they elegantly solve this problem. In the declarative model, the programmer specifies what the user interface should look like, and the computer performs the necessary updates to achieve the programmer's intent. This simplifies the construction of complex user interfaces, because there are none of the side-effects or nondeterminism that is typical of imperatively constructed user interfaces.

	// Presentation, state, and logic are cleanly separated
	// in this example of a declarative user interface
	class FormView extends View
	
	// State:
	bool isLoading
	String inputString

	constructor FormView
		this.isLoading = false
		this.inputString = ""

	// Logic:
	function onButtonClick
		this.isLoading = true

	function onInputChange (newInputString)
		this.inputString = newInputString

	// Presentation:
	function render
		buttonOrNull = null

		if this.input.length > 0
			buttonOrNull = <Button disabled={this.isLoading} onClick={this.onButtonClick}>
				{this.isLoading ? "Loading..." : "Done"}
			</Button>

		return <View>
			<TextInput disabled={this.isLoading} onChange={this.onInputChange}>
				{this.inputString}
			</TextInput>
			{buttonOrNull}
		</View>

This example achieves the same effect as the earlier example in a declarative way. Instead of manipulating instances of `Button` and `TextInput`, the view has a `render`  function that returns a _description_ of what the user interface should look like given the current state of the application. A separate library takes this description and makes the necesscary changes happen on screen. In the declarative model **the user interface is a pure function of the application state**. This makes it much easier to understand how a user interface behaves.
