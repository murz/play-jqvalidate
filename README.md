# play-jqvalidate

Client-side form validation based on your [Play](http://playframework.org) model validation annotations.

## Quick Demo

[http://play-jqvalidate.appspot.com/](http://play-jqvalidate.appspot.com/) is an example form using this module for client-side validation. The source code is available in the `samples-and-tests` folder.

## Dependencies

The `play-jqvalidate` JavaScript components depend on the [jQuery](http://jquery.com/) library.

## Installation

### Install the module

Install the jqvalidate module from the modules repository:

    play install jqvalidate

### Enable the module

After installing the module, add the following to your `application.conf` to enable it:

    module.jqvalidate=${play.path}/modules/jqvalidate

## Usage

### Include the module JavaScript

The module JavaScript file is at `lib/play-jqvalidate.min.js`. This script needs to be copied to your static directory or CDN and included anywhere on your page. The module JavaScript contains compressed copies of the [jQuery Validation Plugin](http://bassistance.de/jquery-plugins/jquery-plugin-validation/) and the [jQuery Metadata Plugin](http://plugins.jquery.com/project/metadata). 

### Use the `jqvalid.form` tag in your view

The `jqvalid.form` tag is identical to the built-in Play form tag except it outputs some JavaScript that prepares the form to be validated by the jQuery validation plugin.

### Use the `jqvalid.field` tag in your view

The `jqvalid.field` tag is identical to the built-in Play field tag except it puts an extra property on the field, `field.validationData`. You need to put this data in an HTML5 data attribute called `data-validate` on your `input`, `select`, or `textarea` element.  

    #{jqvalid.field 'task.details'}
		<p>
	  		<label>&{field.name}</label>
	  		<input type="text" data-validate="${field.validationData}" id="${field.id}" name="${field.name}" value="${field.value}" class="${field.errorClass}">
	  		<span class="error">${field.error}</span>
		</p>
	#{/}
	
## Supported Annotations

The module currently supports the following annotations:

* `Required`
* `Email`
* `Min`
* `Max`
* `Range`
* `MinSize`
* `MaxSize`
* `URL`

## Example

### Model

	@Entity
	public class Task extends Model {
	    @Required @Range(max=10,min=1) public int priority;
	    @Required @Email public String authorEmail;
	    @Required @URL public String authorUrl;
	    @Required public String details;
	}

### View
	
	#{jqvalid.form @Tasks.save()}
	  	#{jqvalid.field 'task.details'}
			<p>
			  <label>&{field.name}</label>
			  <input type="text" data-validate="${field.validationData}" id="${field.id}" name="${field.name}" value="${field.value}" class="${field.errorClass}">
			  <span class="error">${field.error}</span>
			</p>
		#{/}
		#{jqvalid.field 'task.priority'}
			<p>
			  <label>&{field.name}</label>
			  <input type="text" data-validate="${field.validationData}" id="${field.id}" name="${field.name}" value="${field.value}" class="${field.errorClass}">
			  <span class="error">${field.error}</span>
			</p>
		#{/}
		#{jqvalid.field 'task.authorEmail'}
			<p>
			  <label>&{field.name}</label>
			  <input type="text" data-validate="${field.validationData}" id="${field.id}" name="${field.name}" value="${field.value}" class="${field.errorClass}">
			  <span class="error">${field.error}</span>
			</p>
		#{/}
		#{jqvalid.field 'task.authorUrl'}
			<p>
			  <label>&{field.name}</label>
			  <input type="text" data-validate="${field.validationData}" id="${field.id}" name="${field.name}" value="${field.value}" class="${field.errorClass}">
			  <span class="error">${field.error}</span>
			</p>
		#{/}
		<p>
			<input type="submit" value='Create Task'>
		</p>
	#{/jqvalid.form}

### Result

You can view the example form live at [http://play-jqvalidate.appspot.com/](http://play-jqvalidate.appspot.com/). The complete source code is available in this module's `samples-and-tests` folder.



	