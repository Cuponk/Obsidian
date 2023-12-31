
## What is TDD?

![tdd](https://aa-ch-lecture-assets.s3.us-west-1.amazonaws.com/rspec/tdd.png)

---

## #RSpec

+ Domain-Specific Language (DSL) written in Ruby for Ruby
+ Meta-gem that includes `rspec-core`, `rspec-expectations` and `rspec-mocks`
+ Not the only Ruby testing library (others include `Minitest` and `Cucumber`).

### Rspec-rescources

- [Better Spec Cheatsheet](https://www.betterspecs.org/)
- [Rspec Matchers](https://rubydoc.info/github/rspec/rspec-expectations/RSpec/Matchers/BuiltIn/)
---

## RSpec Demo

+ Setup
+ Structure
+ Syntax
   + `describe`, `context`
   + `it`
   + `expect`
   + `before`
   + `subject`
   + `let`

---
#### Piece.rb

```ruby
class Piece
  attr_reader :color, :position, :board
  
  def initialize(color, pos, board)
    raise 'Invalid color' unless [:white, :black].include?(color)
    raise 'Invalid position' unless board.valid_pos?(pos)
    @color = color
    @position = pos
    @board = board
  end

  def symbol
    nil
  end

  def to_s
    symbol
  end
end
```

#### Piece_spec.rb

```ruby
# require_relative '../lib/piece.rb'
require 'piece'

describe Piece do
  let(:board) { double("Board", valid_pos?: true) }
  subject(:piece) { Piece.new(:white, [0,0], board) }
  let(:invalid_piece) { Piece.new(:blue, [0,0], board) }
  # subject and lets are lazily loaded
  # use doubles to primarily mock interactions with other classes

  describe '#initialize' do
    context 'with valid arguments' do
      it 'instantiates instance variables and defines readers' do
        # we write expect statements to enforce a spec
        expect(piece.color).to be(:white)
        expect(piece.position).to eq([0,0])
        expect(piece.board).to be(board)
        # be matcher checks for object equality
        # eq matcher checks for value equality
      end    

      it 'confirms with board that position is valid' do
        expect(board).to receive(:valid_pos?).with([0,0]).and_return(true)
        piece
      end
    end

    context 'with invalid arguments' do
      it 'raises an error when provided an invalid color' do
        # when writing code that we expect to throw an error
        # must pass it to expect in a block
        expect { invalid_piece }.to raise_error('Invalid color')
      end

      # it 'confirms with board that position is valid' do
      #   allow(board).to receive(:valid_pos?).and_return(false)
      #   # expect(board).to receive(:valid_pos?).with([0,0]).and_return(true)
      #   piece
      # end
    end

  end

  describe '#to_s' do
    it 'returns a formatted string' do
      # allow keyword lets us mock certain behavior
      allow(piece).to receive(:symbol).and_return('♜')
      expect(piece.to_s).to eq('♜')
    end
  end
end
```
