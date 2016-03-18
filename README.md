# Passport Strategy for Dataporten

[Passport](https://github.com/jaredhanson/passport) strategy for authenticating
with [Dataporten](http://dataporten.no) using the OAuth 2.0 API.

This is an updated version of the strategy for Feide Connect. Feide Connect was the pilot service for Dataporten. Dataporten went into production in March 2016.


## Install

TODO: Not published to NPM yet. Will do when ready...

	$ npm install passport-dataporten

## Usage

#### Configure Strategy

The Feide Connect authentication strategy authenticates users using a Feide Connect
account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which
accepts these credentials and calls `done` providing a user, as well as
`options` specifying a client ID, client secret, and callback URL.

	passport.use(new DataportenStrategy({
			clientID: CLIENT_ID,
			clientSecret: CLIENT_SECRET,
			callbackURL: 'https://www.example.net/auth/feideconnect/callback'
		},
		function(accessToken, refreshToken, profile, done) {
			User.findOrCreate({ id: profile.id }, function (err, user) {
				return done(err, user);
			});
		}
	));

#### Authenticate Requests

Use `passport.authorize()`, specifying the `'feideconnect'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

	app.get('/auth/feideconnect',
		passport.authorize('feideconnect'));

	app.get('/auth/feideconnect/callback',
		passport.authorize('feideconnect', { failureRedirect: '/login' }),
		function(req, res) {
			// Successful authentication, redirect home.
			res.redirect('/');
		});

## Thanks

- [Jørn Åne](http://github.com/jornane)
- [Jared Hanson](http://github.com/jaredhanson)
- [Andreas Åkre Solberg](http://github.com/andreassolberg)

## License

[The ISC License](http://opensource.org/licenses/ISC)

Copyright (c) 2015 [UNINETT AS](http://github.com/uninett)
