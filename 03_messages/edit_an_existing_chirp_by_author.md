# Edit an existing chirp by author

| URI Pattern | Controller#Action | What should it do? | Example action code |
| -- | -- | -- | -- |
| /:author/chirps/:id/edit(.:format) | **chirps#edit** | Show a form for editing an existing chirp from an author | `Chirp.find_by(author: 'some author', id: 'id')` |
