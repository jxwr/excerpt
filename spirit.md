# boost spirit

- spirit.classic: compatible with Spirit V1.8 (namespace boost::spirit::classic)
- spirit.qi: parser library
- spirit.lex: lexer library
- spirit.karma: generator library

- % x : sperate by, `double_ % ','`
- qi::symbols<KeyT, ValT> is a symbol table, can be used as a base class
- rule: a lot like parsec I think, rule<Iterator, Signature, Skipper> r;
- grammar: encapsulates one or more rules, has the same template parameters as the rule
