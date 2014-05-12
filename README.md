Primero gracias a  Tom Coleman y Sacha Greif!!

Merci, thanks, gracias!!

Simplemente asombroso Meteor!

Ejemplo:

Template.postSubmit.events({
	'submit form': function (e) {
		e.preventDefault();

		var post={
			url:$(e.target).find('[name=url]').val(),
			title:$(e.target).find('[name=title]').val(),
			message:$(e.target).find('[name=message]').val()
		};
		Meteor.call('post', post, function(error, id){
			if(error){
				//display the error to the user
				Errors.throw(error.reason);
				if(error.error === 302)
					Router.go('postPage', {_id: error.details})
			}
			else{
				Router.go('postsList');
				}

		});
	}
});

Template.postEdit.events({
	'submit form': function (e) {
		// ...
		e.preventDefault();

		var currentPostId = this._id;

		var postProperties = {
			url:$(e.target).find('[name=url]').val(),
			title:$(e.target).find('[name=title]').val(),

		}

		Posts.update(currentPostId, {$set: postProperties}, function(error){
			if(error){
				Errors.throw(error.reason);
			} else{
				Router.go('postsList');
				//Router.go('postPage', {_id: currentPostId});
			}
		});
	},

	'click .delete': function(e){
		e.preventDefault();

		if(confirm('Delete this post?')){
			var currentPostId = this._id;
			Posts.remove(currentPostId);
			Router.go('postsList');
		}
	}
});

<template name="layout">
  <div class="container">
      {{> header}}
      {{> meteorErrors}}
    <div id="main" class="row-fluid">
      {{> yield}}
    </div>
  </div>
</template>

Posts.update(currentPostId, {$set: postProperties}, function(error){
			if(error){
				Errors.throw(error.reason);
			} else{
				Router.go('postsList');
			}
});


Router.onBeforeAction(function(){ Errors.clearSeen(); });


Simplemente otra forma de programar

Adios drupal, Joomla, Wprdpress!!!

Bienvenido Meteor!!
